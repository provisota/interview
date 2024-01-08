# Scope
1. Library Motivation: Akka Streams is a library to process and transfer a sequence of elements using bounded buffer space. This property is known as boundedness and it allows Akka Streams to handle potentially infinite streams of data in a safe and predictable manner. It provides a way to define and run flexible, reusable pieces of a data processing pipeline, while the library ensures in-memory buffering is kept within configurable bounds.

2. Defining and running streams: In Akka Streams, a stream processing pipeline is defined with a Source (producing data), a Sink (consuming data), and a Flow (transforming data). A RunnableGraph is a special kind of graph that has both unconnected inputs and outputs. Backpressure is a key feature of Akka Streams, ensuring that producers do not overwhelm consumers. Streams materialization is the process of taking a stream blueprint (a graph) and allocating the necessary resources (memory, threads, etc.) to execute it.

```scala
import akka.actor.ActorSystem
import akka.stream.scaladsl._

implicit val system = ActorSystem("QuickStart")
val source = Source(1 to 10)
val sink = Sink.foreach[Int](println)
val flow = Flow[Int].map(_ * 2)
val runnableGraph = source.via(flow).to(sink)
runnableGraph.run()
```

3. Working with graphs: Akka Streams supports complex processing graphs, not just linear ones. Graphs can have multiple input and output ports and can be either cyclic or acyclic. Fan-out stages send elements to multiple downstream stages (like Broadcast, Balance, UnZip), and fan-in stages receive elements from multiple upstream stages (like Merge, Zip, Concat).

```scala
import akka.stream.scaladsl.GraphDSL.Implicits._

val graph = RunnableGraph.fromGraph(GraphDSL.create() { implicit builder =>
  val broadcast = builder.add(Broadcast[Int](2))
  source ~> broadcast.in
  broadcast.out(0) ~> flow ~> sink
  broadcast.out(1) ~> flow.map(_ * 3) ~> sink
  ClosedShape
})
graph.run()
```

4. Relationship with Reactive Streams: Akka Streams is an implementation of the Reactive Streams specification. Reactive Streams is an initiative to provide a standard for asynchronous stream processing with non-blocking backpressure. It defines a set of interfaces (Publisher, Subscriber, Subscription, and Processor) and a protocol for how they should interact. Akka Streams provides a high-level, type-safe API for defining and running streams, while ensuring compliance with the Reactive Streams specification.
# Questions
1. What is Akka Streams and what are the use cases?
2. How to define and run a stream? What are the main components of a stream?
3. What is stream materialization?
4. What are graphs? what are graphs main components? what is the difference between graphs and streams?
5. What is Operator Fusion and what are its consequences?
6. Can akka streams interoperate with RxJava or SpringReactor? (Interoperation with other Reactive Streams implementations)
# Answers
1. Akka Streams is a library for processing and transferring a sequence of elements using bounded buffer space. This property, known as boundedness, allows Akka Streams to handle potentially infinite streams of data in a safe and predictable manner. It provides a way to define and run flexible, reusable pieces of a data processing pipeline. Use cases for Akka Streams include real-time data processing, implementing backpressure in systems, and any scenario where you need to process a stream of data in a controlled way.

2. In Akka Streams, a stream processing pipeline is defined with a Source (producing data), a Sink (consuming data), and a Flow (transforming data). A Source is a processing stage that has exactly one output, a Sink has exactly one input, and a Flow has exactly one input and one output. You define a stream by connecting these components and then you run it.

3. Stream materialization is the process of taking a stream blueprint (a graph) and allocating the necessary resources (memory, threads, etc.) to execute it. When you run the stream, it materializes the blueprint into a set of live actors that process the stream.

4. Graphs in Akka Streams are a way to define complex streams. They can have multiple input and output ports and can be either cyclic or acyclic. The main components of a graph are Junctions and Modules. Junctions are fan-in or fan-out points in a graph, and Modules are reusable pieces of a graph. The difference between graphs and streams is that streams are linear pipelines of processing stages, while graphs can have a more complex shape with multiple inputs and outputs.

5. Operator Fusion is an optimization that Akka Streams can perform to reduce the overhead of message passing between stages. It merges multiple stages into a single stage, reducing the need for asynchronous message passing. However, it can lead to thread starvation if a fused stage blocks for a long time.

6. Yes, Akka Streams can interoperate with other Reactive Streams implementations like RxJava or Spring Reactor. The Akka Streams API includes methods to create a Source, Sink, or Flow from a Reactive Streams Publisher, Subscriber, or Processor. This allows you to integrate Akka Streams with other libraries that support the Reactive Streams standard.