# System-Design-Notes

## Key Concepts:
- **Scalability:** Can the system handle more users if demand increases?
- **Latency:** How quickly does the system respond to a user request?
- **Throughput:** How much data can be processed at once?
- **Availability:** Can users access the system at all times?
- **Consistency:** Is the data the same for every user?

---

## A. Networking Basics:
- **DNS (Domain Name System):** Converts website names (like google.com) into IP addresses.
- **Load Balancers:** Distribute traffic across multiple servers.
- **HTTP/HTTPS:** Protocols for communication between browsers and servers.

---

## Storage (Databases):
- **SQL:** Structured data (Banking systems).
- **NoSQL:** Unstructured data (Facebook posts, chat messages).
- **Caching:** Store frequently accessed data in memory (Redis, Memcached).
- **Partitioning/Sharding:** Split large databases into smaller chunks.

**Real-Life Example:**  
- **Instagram:** User data (profile info) in SQL; photos stored in NoSQL databases.  
- **Caching:** Instagram caches popular posts to avoid fetching them from the database every time.

---

## Processing (Application Logic):
- **Microservices:** Small, independent services handling specific tasks (Netflix – Recommendation engine, video service).
- **Monolith:** One big application (Early-stage startups).
- **Message Queues:** Help handle background tasks (Sending emails or processing videos).  

**Real-Life Example:**  
- **Uber:** Microservices handle payments, location tracking, and notifications independently.

---

## Scaling Techniques:
- **Horizontal Scaling:** Add more servers (Scale out).
- **Vertical Scaling:** Add more power (CPU, RAM) to a server (Scale up).
- **CDNs (Content Delivery Networks):** Distribute content geographically to reduce load and latency.

**Real-Life Example:**  
- **YouTube:** Uses CDNs to cache videos closer to users, making streaming faster and reducing lag.

---

## Consistent Hashing:

### How Consistent Hashing Works:
- **Hashing the Servers/Nodes:**  
  Each server is assigned a point on a circular hash ring based on a hash of its identifier (like IP or name).
- **Hashing the Data/Keys:**  
  Each data item (key) is also hashed and placed on the same ring.
- **Data Assignment:**  
  A data item is assigned to the next server in a clockwise direction from its position on the ring.

### Node Addition/Removal:
- **Adding a Node:**  
  The new node takes over responsibility for some data from the next node clockwise. Only a small portion of the data needs to be redistributed.
- **Removing a Node:**  
  The data from the removed node gets reassigned to the next node in the clockwise direction. Again, minimal redistribution occurs.

### Example:
- **Content Retrieval:**  
  A user from Europe requests Video1. The system checks the ring and routes the request to the London server, as it is the next node clockwise.
- **Adding a New Server:**  
  A new server in Paris is added. Now, some data previously stored on the London server shifts to Paris, but most of the data distribution remains unchanged.
- **Server Failure:**  
  If the Tokyo server goes offline, the data shifts to the next server (New York), ensuring continued availability with minimal rehashing.

### Key Benefits of Consistent Hashing:
- **Scalability:** Nodes can be added or removed with minimal disruption.
- **Fault Tolerance:** System remains operational even if some nodes fail.
- **Load Balancing:** Data is distributed evenly across nodes.

