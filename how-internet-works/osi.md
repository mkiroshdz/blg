# How the Internet Works, from Basics to HTTP: OSI Model

After six (plus) years working as a web developer, I’ve come to realize that staying relevant isn’t about chasing every new technology out there. Things are always changing in the tech landscape, and while some tools and frameworks stick around, plenty of them don’t. Trying to learn everything isn’t nearly as rewarding—or practical—as understanding the problems these tools are meant to solve and why they were created in the first place.

For me, really understanding how HTTP works is one of those things that gives you a much better sense of where you stand as a developer. It helps you see the bigger picture of web development, the limitations of our current technology, and the possibilities it opens up for the future.

This article is the first in a series aimed at understanding how HTTP works and the stack of technologies that power what we know today as the internet. We’ll explore these topics from a more abstract perspective before diving into the concrete details, ultimately arriving at HTTP.

With that in mind, the first topic we’ll delve into is the OSI model. OSI stands for Open Systems Interconnection and provides an abstraction that explains how software applications exchange messages or data over a network. It breaks this process down into several layers: physical, data link, network (IP), transport, and application.

At this point, the OSI model might sound very platonic, but in this article, I’ll break it down in a more practical way. Let’s dig in!

## Application

I think a more practical way of understanding the layers in the OSI model is to think of them as "concerns." The reason this model is designed in layers, to begin with, is that communication over a network is incredibly complex. To manage that complexity, the process was divided into a series of smaller problems—or concerns—that work together to solve the larger problem of network communication.

Let’s think about a practical example: loading a web page. For simplicity, let’s imagine the server somehow already knows that you want the content of the page and plans to send it to you. The first challenge for both you and the server is figuring out how to share that content in a way your computer can understand—specifically, so it knows what it is and what to do with it, like displaying the page on your screen.

To make this work, both parties must use a common set of rules or instructions that your program can interpret. This is where HTTP comes in. It allows both parties to exchange web pages as a set of tags that have the same meaning for any browser. This part of the problem focuses on shared symbols or a language that only makes sense in the context of the application that wants to communicate—hence the name **application layer**.


## Transport

Having established the specific data to be transmitted, we now face other problems to address. For the sake of simplicity, let’s imagine the most basic scenario: you are directly connected to the other party through a point-to-point connection. In this case, the other party could just transmit the entire message to you one byte after another. However, this approach assumes something significant: there’s no chance of losing any bits during transmission, and all bits will be delivered exactly as they were sent. In other words, we’re assuming the communication channel is completely reliable.

We know that achieving a completely reliable communication channel is extremely difficult—unless you have full control over the physical medium and can isolate it to minimize any chance of interference. Even then, it’s not always practical. Additionally, having a direct connection to every possible server or person you’d want to communicate with over the internet would be impossible. Fortunately, the latter isn’t a new problem—we tackled it long ago.

When we transitioned from point-to-point communications over telegraph systems to switching systems, and later in the 1960s to digital switching, we made a significant leap. Digital switching paved the way for the internet by enabling data to traverse multiple hops, routing packets to reach any connected destination. This advancement came with a crucial limitation: no single communication could monopolize the channel. Everyone needed to share the channel simultaneously; otherwise, it would not work.

To share the channel effectively, the solution was to send data in minimal, discrete pieces that could move quickly through each hop while coexisting with many other pieces of data from different sources—all sharing the same channel. Of course, this approach requires that these discrete packets be reassembled when they reach their destination, and it also demands mechanisms to ensure this process happens correctly.

This is the task of the **transport layer**: figuring out how to move payloads that can be extremely large (sometimes gigabytes in size) while ensuring they can coexist with other communications. The transport layer’s job is to make sure data is split into manageable packets and that everything arrives in the right order, without collisions or loss, even when multiple communications are happening simultaneously.

## Network Layer (IP Layer)

Having the transport of data sorted out, we still need a way for the network's hops to figure out how to route the pieces of our data to reach the correct destination. It’s similar to how we use addresses when sending a physical package through a courier.

Instead of street addresses, however, the internet uses something called **IP addresses**. These are numerical labels that refer to specific destinations within the network. The task of determining how data packets are routed from one point to another, based on these addresses, is handled by the **network layer**, or more specifically, the **IP layer**.

## Data Link and Physical Layers

At this point, we’ve solved most of the problems required to send data across the network. The last remaining task is to actually transmit the message in the physical world. This means translating all those bits into signals—such as electrical pulses or light waves—with the appropriate properties so they can be interpreted by the next hop. 

While it might seem logical to package this concern entirely into the **physical layer**, it turns out the reality is much more complex. Not every hop in the network relies on the same physical medium. Some hops use optical fiber, others rely on electrical cables, and some even transmit data wirelessly. Because of this lack of uniformity, the way bits are translated into physical signals—and then back into bits—varies depending on the medium.

This is where the **data link layer** comes into play. The data link layer handles the unique adaptations required for each type of physical medium. It ensures that bits are translated to and from the physical signals correctly, depending on the technology being used. Meanwhile, the actual signals traveling through physical devices—whether they’re light pulses, electrical currents, or radio waves—are the responsibility of the **physical layer**.

## The Missing Layers

If you’re already familiar with the OSI model, you’ve probably noticed that I skipped two layers that live between the application layer and the transport layer: the **session layer** and the **presentation layer**. While these layers are important, I don’t think they’re mandatory for understanding how to break down the OSI model into its basic concerns.

I’ll probably dedicate an article to these two layers later, as they play a more abstract but still significant role in network communication. For now, we can move forward without them.
