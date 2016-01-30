---
layout: post
title:  "Core Data Gotcha: Objects in Child Contexts Don't Receive Permanent IDs From a Save"
date:   2014-04-08 00:00:00 -0800
---
With the introduction of child contexts since iOS 5, a typical Core Data stack is to create a parent `NSManagedObjectContext` with a concurrency type of `NSPrivateQueueConcurrencyType`, and also create a child context from it with a concurrency type of `NSMainQueueConcurrencyType`. The UI thread would use the child context whenever it needs to work with Core Data objects, while data persistence will happen in the parent context. This setup allows the application to persist data to disk without blocking the UI thread.

Now, I'm questioning whether this is the proper setup. It seems that child contexts are probably not intended to be used like that, and as a result, I ran into a issue of keeping the child and parent fully synchronized. In one of the iOS apps I'm developing, I discovered `NSManagedObject`s in the child context do not receive a permanent `NSManagedObjectID` upon a save that propagates all the way to the parent. In other words, if you do the following:

1. Create a new object in the child context
2. Save the child context
3. Save the parent context (to persist to disk)
4. The newly created object in the child context will not update its temporary ID to the permanent one assigned by the persistence store when the parent is saved. Only the object in the parent context will be updated to reflect the new ID. The object in the child context will remain with a stale temporary ID. The reason why this is an issue is that the UI thread may continue working with the child context and if it happens to pass along the object's ID to other components, the object will not be found.

It seems that this behavior is by design, though in my opinion, it's not intuitive. I see three solutions to this issue:

1. Call `obtainPermenantIDForObjects:error` before saving the child and parent contexts.
2. Discard the child context after a save to parent. I believe this is the intended use of parent-child contexts.
3. Listen to `NSManagedObjectContextObjectsDidChangeNotification` & `NSManagedObjectContextDidSaveNotification` notifications from the parent and refresh & merge objects respectively into the child context.

Since it seems like the intended use of child contexts is to only use them temporarily, I've actually went back to using the traditional model of having two independent contexts (one for the background thread and one for the main thread), each using the same persistence store. Creating a new child for each screen and managing change notification objects didn't seem worthwhile. However, I still use a child context for create/update screens, where changes made by the user can be cancelled. This is where the advantages of child contexts truly shine.
