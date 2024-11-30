# How the Internet Works, from Basics to HTTP: Deconstructing the OSI Model

After six (plus) years working as a web developer, I’ve come to realize that staying relevant isn’t about chasing every new technology out there. Things are always changing in the tech landscape, and while some tools and frameworks stick around, plenty of them don’t. Trying to learn everything isn’t nearly as rewarding—or practical—as understanding the problems these tools are meant to solve and why they were created in the first place.

For me, really understanding how HTTP works is one of those things that gives you a much better sense of where you stand as a developer. It helps you see the bigger picture of web development, the limitations of our current technology, and the possibilities it opens up for the future.

This article is the first in a series aimed at understanding how HTTP works and the stack of technologies that power what we know today as the internet. We’ll explore these topics from a more abstract perspective before diving into the concrete details, ultimately arriving at HTTP.

Before we dive into the technical details—and because the subject can get quite complex—let’s set up the simplest possible scenario to help us understand the basics. We’ll add layers of complexity as we go. Imagine that the entire internet resides in a single magical box connected directly to your computer, like a point-to-point connection. Your goal is to retrieve the contents of **www.somedomain.com**. Let’s call this magical box the **server**, since its purpose is to serve the content of the webpage to your machine.

---

## Point to Point

To understand how the server interacts with your computer, we’ll begin by looking at the **OSI model** (Open Systems Interconnection model). The OSI model is an abstraction that describes the processes required for your computer to send and receive data over a network. For simplicity, we’ll assume the server already knows you want the content of **www.somedomain.com** and will send it to you in one-way communication.

For this communication to happen, the OSI model outlines a series of strictly ordered stages, known as **layers**. These layers are: **Application**, **Transport**, **Data Link**, and **Physical**.

At first glance, the OSI model might seem very abstract. However, one way to make it more understandable is to think of each layer as addressing a specific concern. The reason this model is designed in layers is that network communication is incredibly complex. Breaking it into smaller, more manageable problems—or concerns—makes it easier to understand and work with.

The **Application layer** addresses the first concern: Whether you’re navigating a webpage, reading your email, or making a video call, the computer only sees the data transmitted, nothing more. Beyond receiving it, your machine needs to know how to interpret the data and what to do with it. To make this possible, the server and your computer must share a common set of instructions that allow the data to make sense within the application you’re using.

This is where the **Application layer** comes into play. It ensures that both the server and your machine "speak" a language that makes the data meaningful for the application. For example, consider **HTTP**. I won’t dive too deeply into HTTP here, but it’s a protocol designed specifically for browsing content on the web. It organizes data in a specific format, enabling your browser to understand whether it’s a webpage, an image, audio, or something else. Once your browser understands this, it can display the data appropriately. Since HTTP only makes sense in the context of a browser, it’s classified as a protocol that operates at the **Application layer** of the OSI model.

The data produced by the application layer determines **what** will be sent to your computer, but the **how** is still undecided at this point. The first idea that comes to mind is as simple as our scenario: sending the data in order, bit by bit. It sounds reasonable, but it assumes a connection that will never experience interference, which could interrupt the sequential flow of data. Furthermore, if someone cuts the connection while the server is transmitting, we would simply assume that everything was fine since the server completed its transmission. This concern pertains to the **Transport layer**.

We know that achieving a completely reliable communication channel is extremely difficult—unless you have full control over the physical medium and can isolate it to minimize any chance of interference. Even then, it’s not always practical. The transport layer is responsible for implementing mechanisms that allow communication over an unreliable medium. This translates to: finding a way to ensure the message actually reached its destination (**acknowledgment**) and being able to retransmit it if necessary.

The solution here involves having your machine send an acknowledgment message back to the server. If the server doesn’t receive acknowledgment within a certain timeframe, it will need to retransmit the **entire message**. This means that if the message is megabytes or gigabytes long, the server will have to resend everything from the start, which is far from optimal.

To recover effectively from disconnection, dividing the whole message into discrete, smaller packets is much more convenient. This approach allows your machine to acknowledge each packet individually and identify exactly which parts of the transmission are missing. The server can then retransmit only the missing packets instead of the entire message. This responsibility also falls under the **Transport layer**. In summary, the transport layer controls the flow of packets by enabling acknowledgment and recovery mechanisms.

At this point, we’ve solved most of the problems required to send data. The last remaining task is to actually transmit the message in the physical world. This means translating all those bits into signals that can vary depending on the interface our point-to-point connection uses. It could transmit using optical fiber, rely on electrical pulses, or even transmit wirelessly. Each of these physical mediums requires a layer that knows exactly how to generate and interpret those physical signals appropriately and check the correctness of the transmission due to the possibility of flipped bits. This translation layer is known as the **Data Link layer**.

The final requirement of our transmission is to actually have a physical link to connect our machine and the server, which we call the **Physical layer**. And voila! With all these concerns solved, we can transmit for our basic scenario. While this is obviously not how the internet works, it gives us a fair idea of the most basic concerns when transmitting.

---

## Internet Protocol (IP)

To make our scenario more aligned with how the internet works today, we need to break our magic box into millions of machines that serve content to us. These machines are distributed across different geographical locations, and among them, the content of millions of domains is stored (included www.somedomain.com). Having direct point-to-point connections from our machine to each one of these servers is simply impossible.

This problem was solved when we transitioned from point-to-point communications over telegraph systems to switching systems, and later in the 1960s, to digital switching. Digital switching paved the way for the internet by enabling data to traverse multiple hops, routing packets to reach any connected destination. This change not only made the internet scalable but also resilient to disconnections between hops due to redundancy.

Having this new layer of hops between our machine and the server makes our previous solution insufficient. We cannot simply transmit directly; we need to transmit from hop to hop using the correct route to reach our destination. For that, we need a way to determine the correct path, similar to the addresses we use when sending packages via courier services. To tackle this issue, another concern should be added to the model: the **Network layer**, just above the data link layer.

Similar to streets, every hop connected to the network contains several addresses that correspond with the neighboring hops. Every hop in the network is intelligent enough to decide which neighbor is the most appropriate to route toward the hop that contains the target address. Such addresses on the network layer are known as **IP addresses** and, in essence, are just a numeric label composed of 12 binary digits.

---

## The Missing Layers

If you’re already familiar with the OSI model, you’ve probably noticed that I skipped two layers that live between the application layer and the transport layer: the **session layer** and the **presentation layer**. While these layers are important, I don’t think they’re mandatory for understanding how to break down the OSI model into its basic concerns.

I’ll probably dedicate an article to these two layers later, as they play a more abstract but still significant role in network communication. For now, we can move forward without them.
