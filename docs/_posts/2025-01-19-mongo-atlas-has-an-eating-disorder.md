---
layout: post
title: "Mongo Atlas Has an Eating Disorder"
author: Amin
tags: [software development, cloud, database]
---

I’ve been building side projects with Mongo Atlas since 2022 (before that, I generally used PostgreSQL).

The main reason I switched to Mongo was the ease of use and seamless integration with JS environments, which I mainly code in.

The Mongo Atlas free shared cluster made it super easy to get started.

It’s been three years, and I’m still using MongoDB and continue to be amazed by the extra goodies you get for free from Mongo Atlas (the M0 shared cluster, which has 512MB of storage and limited processing power).

## What’s been most amazing with Mongo Atlas is the Application Services.

Application Services are a group of services that push beyond the standard capabilities of MongoDB itself, allowing you to define serverless functions, database triggers, and even HTTP endpoints that are directly served from your cluster.

You can also manage your entire Application Services using **IaC**, and they have a nice integration with **GitHub**, which allows automatic two-way syncing between your Atlas cloud and your code.

---

It wasn’t perfect, though. I think they’re still on **Node 10**, which is ancient in the JS world, and as a result, many package dependencies just wouldn’t work.

Also, everything around the serverless functionality—e.g., logging, metrics, debugging—is just lacking.

To make it even worse, they have been deprecating some of the goodies recently, e.g., the **HTTP service**.

---

There are also some restrictions on shared clusters that sometimes seem unnecessary. For example, you won’t have access to the previous version of changed documents in triggers if you’re using the shared cluster.

It “feels” like they want to push me toward a **dedicated cluster** (which is way more expensive than shared) in sneaky ways, even if I won’t need it anytime soon with my usage pattern.

### Cluster Bloat

Mainly by imposing stricter rate limiting, removing critical features, and **Cluster Bloat** (as I call it).

**Cluster bloat** is sneaky, and you won’t notice it until you've been inserting new documents for a while.

#### How does it happen?

- Deleting documents won’t free up space in Mongo.
- You can manually remove those by running the `compact` command.
- The `compact` command is not allowed on a shared cluster!

So, basically, the moment your DB starts reaching the maximum storage (512MB), you have no option but to migrate to a larger cluster until you run out of capacity on the largest shared cluster (5GB) as well.

You then must switch to a dedicated cluster to keep your DB usable (and the price more than doubles).

---

When I first faced this problem, I thought, *"OK, I’ll upgrade. I’ll pay more but at least have some peace of mind for a while."*

But when I did, something terrible happened: my triggers stopped working, and there was no way to delete or override them.

I had to restore everything from backup!

---

I also thought about their serverless option, which sounds very tempting to me. But unfortunately, it doesn’t have any of the nice features you get from Application Services and **Atlas Search**.

It’s a shame because I really like my experience with Mongo Atlas, even with the shortcomings, and how cost-effective it was, allowing me to take my time with the usage and development.

I’m now looking for alternatives, and **Cloudflare D1** sounds very interesting.