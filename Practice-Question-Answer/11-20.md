# ☁️ Azure Development & Security Practice Question

--------------------------------------------------------------------------------
📌 Question 11
--------------------------------------------------------------------------------
You are creating an app that uses Event Grid to connect with other services. 
Your app's event data will be sent to a serverless function that checks compliance.

This function is maintained by your company.

You write a new event subscription at the scope of your resource. The event must 
be invalidated after a specific period of time.

You need to configure Event Grid.

What should you do? To answer, select the appropriate options in the answer area.

### Options 
**WebHook event delivery:** (DropDown)
- SAS tokens
- Key authentication
- Management Access Control

**Topic publishing:** (DropDown)
- ValidationCode handshake
- ValidationURL handshake
- JWT token

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. WebHook event delivery: **SAS tokens**
2. Topic publishing: **ValidationURL handshake**

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **WebHook event delivery: SAS tokens**
   - The requirement states that "The event must be invalidated after a 
     specific period of time."
   - **SAS (Shared Access Signature) tokens** are the standard mechanism in 
     Azure for granting time-limited access to resources. By appending a SAS 
     token to the WebHook URL, you ensure that the ability to deliver events 
     to that endpoint expires after the token's validity period.
   - `Key authentication` (like Function Keys) typically involves static keys 
     that do not expire automatically.
   - `Management Access Control` refers to RBAC permissions for managing the 
     resource, not the data plane delivery authentication.

2. **Topic publishing: ValidationURL handshake**
   - This dropdown refers to the **Subscription Validation** process (proving 
     ownership of the WebHook endpoint).
   - When creating an Event Grid subscription to a WebHook, a validation event 
     is sent.
   - The **ValidationURL handshake** involves Event Grid sending a 
     `validationUrl` in the event data. This URL is explicitly valid for a 
     **specific period of time** (typically 5-10 minutes). If not accessed 
     within that window, the validation event "invalidates" (expires).
   - `ValidationCode handshake` involves echoing a code back programmatically 
     and is less focused on a user-clickable, time-bound link concept compared 
     to the URL method in this context.
   - `JWT token` is an authentication method, not a validation handshake 
     mechanism.   

--------------------------------------------------------------------------------
📌 Question 12
--------------------------------------------------------------------------------
You need to configure Azure CDN for the Shipping web site.

Which configuration options should you use? To answer, select the appropriate options in the answer area.

**Tier:**
- Standard
- Premium

**Profile:**
- Akamai
- Microsoft

**Optimization:**
- general web delivery
- large file download
- dynamic site acceleration
- video-on-demand media streaming

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. Tier: **Standard**
2. Profile: **Akamai**
3. Optimization: **dynamic site acceleration**

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **Optimization: dynamic site acceleration**
   - A "Shipping web site" typically involves real-time tracking, status updates, and personalized user data which is highly dynamic and cannot be heavily cached.
   - **Dynamic Site Acceleration (DSA)** is specifically designed to optimize the delivery of dynamic content by using techniques like route optimization and TCP optimization, rather than just caching static assets.

2. **Profile: Akamai**
   - In the context of Azure CDN profiles available in the portal (and exam scenarios), **Azure CDN Standard from Akamai** is a primary provider that supports the specific "Dynamic site acceleration" optimization type.
   - **Azure CDN Standard from Microsoft** is generally optimized for static content delivery and does not offer the specific "Dynamic site acceleration" optimization selection in the same way Akamai and Verizon do.

3. **Tier: Standard**
   - Since the chosen profile is **Akamai**, the only available tier is **Standard**. The "Premium" tier is exclusive to the **Verizon** profile (Azure CDN Premium from Verizon), which is not a valid combination with Akamai.    

--------------------------------------------------------------------------------
📌 Question 13 ⭐⭐⭐
--------------------------------------------------------------------------------
You develop a gateway solution for a public facing news API.

The news API back end is implemented as a RESTful service and hosted in an Azure 
App Service instance.

You need to configure back-end authentication for the API Management service 
instance.

Which target and gateway credential type should you use? To answer, drag the 
appropriate values to the correct parameters.

**Values:**
- Azure Resource
- HTTP(s) endpoint
- Basic
- Client cert

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. Target: **Azure Resource**
2. Gateway credentials: **Client cert**

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **Target: Azure Resource**
   - The backend is explicitly stated to be hosted in an **Azure App Service** 
     instance.
   - When configuring a backend in Azure API Management, selecting **Azure 
     Resource** allows you to directly select the App Service from your 
     subscription. This is the most integrated and manageable approach compared 
     to manually typing a generic `HTTP(s) endpoint`.

2. **Gateway credentials: Client cert**
   - **Client Certificate (Mutual TLS)** is the standard and most secure method 
     for authenticating the API Management gateway to the backend App Service.
   - You can configure the App Service to require a client certificate and then 
     configure API Management to present that certificate (Gateway credential) 
     with each request.
   - **Basic** authentication is typically not a selectable "Gateway credential 
     type" in the API Management backend configuration UI (which prioritizes 
     Client Certs and Managed Identity). Basic auth would usually be handled 
     via policy headers, whereas Client Cert is a first-class configuration 
     option.    

--------------------------------------------------------------------------------
📌 Question 14
--------------------------------------------------------------------------------
You need to retrieve all order line items from Order.json and sort the data 
alphabetically by the city.

How should you complete the code? To answer, select the appropriate options in 
the answer area.

**FROM**
- Orders o
- LineItems li

**JOIN** [Alias] **IN** [Source]
- Alias: `li` or `o`
- Source: `o.line_items`, `li.line_items`, or `o.address`

**ORDER BY**
- o.address.city
- li.address.city
- o.city
- li.city

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. FROM: **Orders o**
2. JOIN: **li**
3. IN: **o.line_items**
4. ORDER BY: **o.address.city**

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **FROM Orders o**
   - The query targets the `Orders` container (aliased as `o`). The source file 
     is `Order.json`, implying the root documents are Orders.

2. **JOIN li IN o.line_items**
   - **JOIN** is used to flatten the `line_items` array inside each order so 
     that each item can be treated as a separate row in the result set.
   - **li** is the alias defined for the individual line item (matching the 
     `SELECT li.id` clause).
   - **IN o.line_items** specifies the array source to iterate over.

3. **ORDER BY o.address.city**
   - The requirement is to sort by city. In standard JSON order schemas (and 
     Azure Cosmos DB exam datasets), the city is typically a property of a 
     nested `address` object on the root Order document (`o`), not on the 
     individual line items (`li`).
   - Therefore, `o.address.city` is the correct path to the sort key.

--------------------------------------------------------------------------------
📌 Question 15
--------------------------------------------------------------------------------
You are developing an Azure messaging solution.

You need to ensure that the solution meets the following requirements:
- Provide transactional support.
- Provide duplicate detection.
- Store the messages for an unlimited period of time.

Which two technologies will meet the requirements? Each correct answer presents a complete solution.

NOTE: Each correct selection is worth one point.

Options:
1. A. Azure Service Bus Topic
2. B. Azure Service Bus Queue
3. C. Azure Storage Queue
4. D. Azure Event Hub

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
A and B

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **Transactional Support:**
   - **Azure Service Bus (Queues and Topics)** supports local transactions. You 
     can group operations (like sending, receiving, and deleting messages) into 
     a single atomic unit.
   - **Azure Storage Queues** and **Event Hubs** do not support transactions 
     in this manner.

2. **Duplicate Detection:**
   - **Azure Service Bus** has a built-in "Duplicate Detection" feature that 
     automatically discards duplicate messages sent within a specific time 
     window based on the `MessageId`.
   - **Azure Storage Queues** and **Event Hubs** do not have native duplicate 
     detection; this must be handled by the application logic.

3. **Unlimited Storage Time:**
   - **Azure Service Bus** allows you to set the `TimeToLive` (TTL) property 
     of a message to `TimeSpan.MaxValue`, effectively allowing messages to be 
     stored indefinitely (as long as the storage quota is not exceeded).
   - **Azure Storage Queues** historically had a 7-day limit, though newer 
     API versions allow infinite TTL. However, they fail the other requirements.
   - **Azure Event Hubs** is a log-based event streamer with a fixed retention 
     period (e.g., 1 to 90 days), not an indefinite message store.

--------------------------------------------------------------------------------
📌 Question 16
--------------------------------------------------------------------------------
You are developing an application that uses Azure Storage Queues.
You have the provided code snippet.

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));
CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

CloudQueue queue = queueClient.GetQueueReference("appqueue");
await queue.CreateIfNotExistsAsync();

CloudQueueMessage peekedMessage = await queue.PeekMessageAsync();
if (peekedMessage != null)
{
    Console.WriteLine("The peeked message is: {0}", peekedMessage.AsString);
}
CloudQueueMessage message = await queue.GetMessageAsync();
```

For each of the following statements, select Yes if the statement is true. 
Otherwise, select No.

**Statements:**
1. The code configures the lock duration for the queue. ⚪ Yes  ⚪ No
2. The last message read remains in the queue after the code runs. ⚪ Yes  ⚪ No
3. The storage queue remains in the storage account after the code runs. ⚪ Yes  ⚪ No

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. The code configures the lock duration for the queue: **No**
2. The last message read remains in the queue after the code runs: **Yes**
3. The storage queue remains in the storage account after the code runs: **Yes**

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **No**: The code calls `queue.GetMessageAsync()` without any arguments. 
   - While `GetMessageAsync` does apply a default visibility timeout (lock) of 
     30 seconds to the *message*, the code does not explicitly "configure" a 
     custom lock duration.
   - Furthermore, lock duration is typically a parameter of the retrieval 
     operation or a property of the message interaction, not a persistent 
     configuration setting on the `CloudQueue` object itself.

2. **Yes**: The code calls `GetMessageAsync()`, which retrieves the message and 
   makes it invisible to other consumers for the visibility timeout period. 
   - Crucially, the code **does not call** `queue.DeleteMessageAsync()`.
   - In Azure Storage Queues, retrieving a message is a two-step process: 
     Get (hide) -> Delete. Since the delete step is missing, the message 
     remains in the queue and will become visible again after the timeout expires.

3. **Yes**: The code calls `CreateIfNotExistsAsync()` to ensure the queue exists.
   - It **does not call** `queue.DeleteAsync()` or `queue.DeleteIfExistsAsync()`.
   - Therefore, the queue resource itself persists in the storage account after 
     execution.

--------------------------------------------------------------------------------
📌 Question 17
--------------------------------------------------------------------------------
You have an application that provides weather forecasting data to external 
partners. You use Azure API Management to publish APIs.

You must change the behavior of the API to meet the following requirements:
- Support alternative input parameters
- Remove formatting text from responses
- Provide additional context to back-end services

Which types of policies should you implement? To answer, drag the policy types 
to the correct requirements.

**Policy types:**
- Inbound
- Outbound
- Backend

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. Support alternative input parameters: **Inbound**
2. Remove formatting text from responses: **Outbound**
3. Provide additional context to back-end services: **Inbound**

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **Support alternative input parameters: Inbound**
   - **Inbound policies** are executed when a request is received from a client 
     but before it is sent to the backend.
   - To support "alternative input parameters" (e.g., mapping a query parameter 
     `?city=London` from the client to a header `X-City: London` expected by 
     the backend, or rewriting the URL), you must modify the incoming request. 
     This is a classic use case for **Inbound** policies like `rewrite-uri`, 
     `set-query-parameter`, or `set-header`.

2. **Remove formatting text from responses: Outbound**
   - **Outbound policies** are executed after the response has been received 
     from the backend service but before it is sent back to the client.
   - To "remove formatting text" (e.g., stripping specific headers, transforming 
     XML to JSON, or using `find-and-replace` to remove sensitive strings from 
     the body), you must modify the outgoing response. This happens in the 
     **Outbound** section.

3. **Provide additional context to back-end services: Inbound**
   - Providing "additional context" typically means injecting extra information 
     into the request that the backend service needs to process the logic (e.g., 
     adding a `User-ID` header derived from a JWT token, or adding a 
     correlation ID).
   - Since this information must be added *before* the request reaches the 
     backend, it is implemented using **Inbound** policies (specifically 
     `set-header` or `set-body`).

--------------------------------------------------------------------------------
📌 Question 18
-------------------------------------------------------------------------------- 
A software as a service (SaaS) company provides document management services. 
The company has a service that consists of several Azure web apps. All Azure 
web apps run in an Azure App Service Plan named PrimaryASP.

You are developing a new web service by using a web app named ExcelParser. 
The web app contains a third-party library for processing Microsoft Excel files.

The license for the third-party library stipulates that you can only run a 
single instance of the library.

You need to configure the service.

How should you complete the script? To answer, select the appropriate options 
in the answer area.

--------------------------------------------------------------------------------
💻 Code & Dropdowns
--------------------------------------------------------------------------------
Set-AzAppServicePlan `
  -ResourceGroupName $rg `
  -Name "PrimaryASP" `
  ▼ [ Select Option 1 ]

$app = Get-AzWebApp `
  -ResourceGroupName $rg `
  -Name "ExcelParser"

$app.▼ [ Select Option 2 ]

Set-AzWebApp $app

--------------------------------------------------------------------------------
🔽 Options for Dropdown 1 & 2
--------------------------------------------------------------------------------
1. [ ] NumberOfSites 1
2. [ ] PerSiteScaling $true
3. [ ] TargetWorkerCount = 1
4. [ ] MaxNumberOfWorkers = 1
5. [ ] SiteConfig.NumberOfWorkers = 1

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. [ Select Option 1 ]: -PerSiteScaling $true
2. [ Select Option 2 ]: SiteConfig.NumberOfWorkers = 1

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. Set-AzAppServicePlan: -PerSiteScaling $true
   • The requirement is to limit a specific app (ExcelParser) to a single 
     instance while allowing other apps in the same App Service Plan 
     (PrimaryASP) to potentially scale out.
   • Per-App Scaling is a feature in Azure App Service that allows you to 
     control the number of instances for individual apps within a plan, 
     independent of the plan's instance count.
   • To enable this, you must first set the -PerSiteScaling parameter to 
     $true on the App Service Plan itself.

2. $app: SiteConfig.NumberOfWorkers = 1
   • Once Per-App Scaling is enabled on the plan, you configure the specific 
     app's instance count using the NumberOfWorkers property within its 
     SiteConfig.
   • Setting $app.SiteConfig.NumberOfWorkers = 1 ensures that the ExcelParser 
     app runs on exactly one worker, satisfying the licensing constraint, 
     even if the underlying App Service Plan scales out to 10 or more 
     instances for other apps.

--------------------------------------------------------------------------------
📌 Question 19
--------------------------------------------------------------------------------
You are developing a .NET application that communicates with Azure Storage.

A message must be stored when the application initializes.

You need to implement the message.

How should you complete the code segment? To answer, select the appropriate 
options in the answer area.

--------------------------------------------------------------------------------
💻 Code & Dropdowns
--------------------------------------------------------------------------------
```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

▼ [ Select Option 1 ] pVar1 = storageAccount.▼ [ Select Option 2 ]();

▼ [ Select Option 3 ] pVar2 = pVar1.▼ [ Select Option 4 ]("contoso-storage");

try
{
    await pVar2.CreateIfNotExistsAsync();
}
catch (StorageException x)
{
    throw;
}

CloudQueueMessage cloudQueueMessage = new CloudQueueMessage("App Launch: <iUserID>");
await pVar2.AddMessageAsync(cloudQueueMessage);
```

--------------------------------------------------------------------------------
🔽 Options
--------------------------------------------------------------------------------
[ Option 1 & 3 Types ]        [ Option 2 & 4 Methods ]
- CloudQueueClient            - CreateCloudQueueClient
- CloudTableClient            - CreateCloudTableClient
- CloudQueue                  - GetQueueReference
- CloudTable                  - GetTableReference

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
1. []: CloudQueueClient
2. []: CreateCloudQueueClient
3. []: CloudQueue
4. []: GetQueueReference

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
The code snippet creates a message (`CloudQueueMessage`) and adds it to a 
storage resource. This indicates the use of **Azure Queue Storage**.

1. **pVar1 (Type): CloudQueueClient**
   - The `CloudStorageAccount` object is the entry point. To work with queues, 
     you need a client object. The correct type for the client is 
     `CloudQueueClient`.

2. **storageAccount (Method): CreateCloudQueueClient**
   - The method on the `CloudStorageAccount` instance that returns a 
     `CloudQueueClient` is `CreateCloudQueueClient()`.

3. **pVar2 (Type): CloudQueue**
   - `pVar2` represents the specific queue itself (named "contoso-storage"). 
     The class that represents a queue and has methods like 
     `CreateIfNotExistsAsync` and `AddMessageAsync` is `CloudQueue`.

4. **pVar1 (Method): GetQueueReference**
   - To get a `CloudQueue` instance from the `CloudQueueClient` (`pVar1`), 
     you use the method `GetQueueReference("queue-name")`.

--------------------------------------------------------------------------------
📌 Question 20
--------------------------------------------------------------------------------
You are creating an app that will use CosmosDB for data storage. The app will 
process batches of relational data.

You need to select an API for the app.

Which API should you use?

A. MongoDB API
B. Table API
C. SQL API
D. Cassandra API

--------------------------------------------------------------------------------
✅ Correct Answer
--------------------------------------------------------------------------------
C. SQL API

--------------------------------------------------------------------------------
📝 Explanation
--------------------------------------------------------------------------------
1. **SQL API (Core / NoSQL):**
   - The **SQL API** is the default and most versatile API for Azure Cosmos DB.
   - Although Cosmos DB is a NoSQL database, the SQL API allows you to query 
     JSON documents using **Structured Query Language (SQL)** syntax (e.g., 
     `SELECT * FROM c WHERE...`).
   - This makes it the best choice among the provided options for handling 
     data that is conceptualized as **relational**, as developers can leverage 
     familiar SQL concepts to query and model the data (using techniques like 
     embedding or referencing to represent relationships).
   - The SQL API also has robust support for **batch operations** (via 
     Transactional Batch in the SDK) and **bulk execution** for processing 
     large volumes of data efficiently.

2. **Why not the others?**
   - **A. MongoDB API:** Designed for compatibility with existing MongoDB 
     applications (document store). While flexible, it doesn't offer the 
     standard SQL query syntax that "relational data" typically implies in 
     this context.
   - **B. Table API:** Designed for **Key-Value** storage. It is too simple 
     for complex relational data structures and lacks rich query capabilities.
   - **D. Cassandra API:** Designed for **Wide-Column** storage, typically 
     used for high-write scenarios like telemetry or time-series data, not 
     general relational data processing.
