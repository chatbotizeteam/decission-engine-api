# Code Block API Methods

This documentation includes all Java Script methods available in Code Block as part of Processes.

**Table of Contents**

- [API for Orders](#api-for-orders-integration)
- [API for Products](#api-for-products-integration)
- [API for Returns](#api-for-returns-integration)
- [API for Subscriptions](#api-for-subscriptions-integration)
- [API for Ticketing](#api-for-ticketing-integration)
- [API for Block](#block)
- [API for CRM](#crm)
- [API for AI](#ai)
- [API for Interaction](#interaction)
- [API for HTTP](#http)
- [API for Block](#block)
- [API for Availability](#availability)

## Block

### block.finish(result?: "success" \| "failure", reason?: string): void

Finishes the current block with the given status. This function does not have to be explicitly called in most cases, as the block will automatically finish when Javascript evaluation completes.

#### Arguments

| Name   | Type                   | Description                                                                                               |
| ------ | ---------------------- | --------------------------------------------------------------------------------------------------------- |
| result | "success" \| "failure" | The completion status of the block. If result is not provided, defaults to success (optional)             |
| reason | string                 | reason; the reason will be printed to session log if result is failure, otherwise it's ignored (optional) |

---

## Interaction

### interaction.getUserInfo(): User

Retrieves the current user's information

#### Returns

User information object

### interaction.getLastIncomingMessage(): Message \| null

Retrieves the last incoming message or null if none

#### Returns

The last message or null if no messages exist

### interaction.getMessages(): Message[]

Retrieves the list of conversation messages

#### Returns

Array of Messages

### interaction.log(message: string, dumpContext?: boolean): void

Logs a message to session log

#### Arguments

| Name        | Type    | Description                                                     |
| ----------- | ------- | --------------------------------------------------------------- |
| message     | string  | The message                                                     |
| dumpContext | boolean | dump the entire context/store into session log (default: false) |

### interaction.getPlaintextTranscript({ timeFrom, timeTo, timezoneOffsetMinutes, hideRealAgentNames, }: { timeFrom?: number; timeTo?: number; timezoneOffsetMinutes?: number; hideRealAgentNames?: boolean; }): string

Retrieves the plaintext transcript of the conversation.

#### Arguments

| Name                          | Type    | Description                                                            |
| ----------------------------- | ------- | ---------------------------------------------------------------------- |
| options                       | object  | Options for retrieving the transcript.                                 |
| options.timeFrom              | number  | The start time (in milliseconds since epoch) to filter the transcript. |
| options.timeTo                | number  | The end time (in milliseconds since epoch) to filter the transcript.   |
| options.timezoneOffsetMinutes | number  | The timezone offset in minutes to adjust timestamps.                   |
| options.hideRealAgentNames    | boolean | Whether to hide real agent names in the transcript.                    |

#### Returns

The plaintext transcript of the conversation.

### interaction.getPlaintextTranscript(): string

Retrieves the plaintext transcript of the conversation.

#### Returns

The plaintext transcript of the conversation.

### interaction.getHtmlTranscript({ timeFrom, timeTo, timezoneOffsetMinutes, hideRealAgentNames, }: { timeFrom?: number; timeTo?: number; timezoneOffsetMinutes?: number; hideRealAgentNames?: boolean; }): string

Retrieves the HTML transcript of the conversation.

#### Arguments

| Name                          | Type    | Description                                                            |
| ----------------------------- | ------- | ---------------------------------------------------------------------- |
| options                       | object  | Options for retrieving the transcript.                                 |
| options.timeFrom              | number  | The start time (in milliseconds since epoch) to filter the transcript. |
| options.timeTo                | number  | The end time (in milliseconds since epoch) to filter the transcript.   |
| options.timezoneOffsetMinutes | number  | The timezone offset in minutes to adjust timestamps.                   |
| options.hideRealAgentNames    | boolean | Whether to hide real agent names in the transcript.                    |

#### Returns

The HTML transcript of the conversation.

### interaction.getHtmlTranscript(): string

Retrieves the HTML transcript of the conversation.

#### Returns

The HTML transcript of the conversation.

### interaction.data.write(key: string, value: any): void

Writes data to the structured session store.

#### Arguments

| Name  | Type   | Description         |
| ----- | ------ | ------------------- |
| key   | string | The key to write to |
| value | any    | The value to write  |

### interaction.data.read(key: string): any

Reads a value from a specific key from the structured session store

#### Arguments

| Name | Type   | Description          |
| ---- | ------ | -------------------- |
| key  | string | The key to read from |

#### Returns

The value or null if the value does not exist

### interaction.data.writeRaw(key: string, value: any): void

Writes data to the raw session store

#### Arguments

| Name  | Type   | Description            |
| ----- | ------ | ---------------------- |
| key   | string | The key to write to    |
| value | any    | The raw value to write |

### interaction.data.readRaw(key: string): any

Reads a value from a specific key from the raw session store

#### Arguments

| Name | Type   | Description          |
| ---- | ------ | -------------------- |
| key  | string | The key to read from |

#### Returns

The raw value or null if the raw value does not exist

### interaction.data.readAll(): Record<string, any>

Reads all values from the structured session store

#### Returns

Object containing all key-value pairs

### interaction.data.readAllRaw(): Record<string, any>

Reads all values from the raw session store

#### Returns

Object containing all key-value pairs

---

## CRM

### crm.write(key: string, value: any): void

Writes a single value to the CRM

#### Arguments

| Name  | Type   | Description         |
| ----- | ------ | ------------------- |
| key   | string | The key to write to |
| value | any    | The value to write  |

### crm.writeMany(data: Record<string, any>): void

Writes multiple values to the CRM

#### Arguments

| Name | Type                | Description                                |
| ---- | ------------------- | ------------------------------------------ |
| data | Record<string, any> | Object containing multiple key-value pairs |

### crm.getUser(): CrmUser

Retrieves the current user's information Contains data written to the CRM earlier via write/writeMany, as well as default parameters that exist on the User object and parameters set by other parts of the system

#### Returns

User information object

---

## AI

### ai.completions.generate(prompt: string): { outcome: "success" \| "failure", value: string \| null }

Generates a completion for a given prompt

#### Arguments

| Name   | Type   | Description      |
| ------ | ------ | ---------------- |
| prompt | string | The input prompt |

#### Returns

An object with outcome and llm response
| Name | Type |
| - | - |
| outcome | "success" \| "failure" |
| value | string \| null |

### ai.completions.generate(prompt: string, config?: { asJson?: boolean }): { outcome: "success" \| "failure", value: object \| string \| null }

Generates a completion for a given prompt

#### Arguments

| Name          | Type    | Description                                                      |
| ------------- | ------- | ---------------------------------------------------------------- |
| prompt        | string  | The input prompt                                                 |
| config        | object  | The optional configuration object for the request                |
| config.asJson | boolean | Whether to return the response as a JSON object (default: false) |

#### Returns

An object with outcome and llm response
| Name | Type |
| - | - |
| outcome | "success" \| "failure" |
| value | object \| string \| null |

### ai.intents.recognize(message: string): IntentResult \| null

Recognizes the intent of a given message

#### Arguments

| Name    | Type   | Description       |
| ------- | ------ | ----------------- |
| message | string | The input message |

#### Returns

Intent recognition result or null

---

## HTTP

### http.get(url: string, config?: { headers?: Record<string, string>; timeout?: number }): HttpResponse

Sends a GET request to the specified URL

#### Arguments

| Name           | Type                   | Description                                                                       |
| -------------- | ---------------------- | --------------------------------------------------------------------------------- |
| url            | string                 | The URL to send the request to                                                    |
| config         | object                 | The optional configuration object for the request (optional)                      |
| config.headers | Record<string, string> | Optional headers (key-vaue pairs) to include in the request                       |
| config.timeout | number                 | The timeout in milliseconds (default: 30000). The maximum allowed value is 30000. |

#### Returns

The HTTP response

### http.post(url: string, config?: { headers?: Record<string, string>; data: any; timeout?: number }): HttpResponse

Sends a POST request to the specified URL with the given configuration.

#### Arguments

| Name           | Type                   | Description                                                                       |
| -------------- | ---------------------- | --------------------------------------------------------------------------------- |
| url            | string                 | The endpoint to send the request to.                                              |
| config         | object                 | The optional configuration object for the request.                                |
| config.headers | Record<string, string> | Optional headers (key-vaue pairs) to include in the request                       |
| config.data    | any                    | The payload to send in the request body.                                          |
| config.timeout | number                 | The timeout in milliseconds (default: 30000). The maximum allowed value is 30000. |

#### Returns

The HTTP response

### http.put(url: string, config?: { headers?: Record<string, string>; data: any; timeout?: number }): HttpResponse

Sends a POST request to the specified URL with the given configuration.

#### Arguments

| Name           | Type                   | Description                                                                       |
| -------------- | ---------------------- | --------------------------------------------------------------------------------- |
| url            | string                 | The endpoint to send the request to.                                              |
| config         | object                 | The optional configuration object for the request.                                |
| config.headers | Record<string, string> | Optional headers (key-vaue pairs) to include in the request                       |
| config.data    | any                    | The payload to send in the request body.                                          |
| config.timeout | number                 | The timeout in milliseconds (default: 30000). The maximum allowed value is 30000. |

#### Returns

The HTTP response

### http.patch(url: string, config?: { headers?: Record<string, string>; data: any; timeout?: number }): HttpResponse

Sends a PATCH request to the specified URL with the given configuration.

#### Arguments

| Name           | Type                   | Description                                                                       |
| -------------- | ---------------------- | --------------------------------------------------------------------------------- |
| url            | string                 | The endpoint to send the request to.                                              |
| config         | object                 | The optional configuration object for the request.                                |
| config.headers | Record<string, string> | Optional headers (key-vaue pairs) to include in the request                       |
| config.data    | any                    | The payload to send in the request body.                                          |
| config.timeout | number                 | The timeout in milliseconds (default: 30000). The maximum allowed value is 30000. |

#### Returns

The HTTP response

### http.delete(url: string, config?: { headers?: Record<string, string>; timeout?: number }): HttpResponse

Sends a DELETE request to the specified URL with the given configuration.

#### Arguments

| Name           | Type                   | Description                                                                       |
| -------------- | ---------------------- | --------------------------------------------------------------------------------- |
| url            | string                 | The endpoint to send the request to.                                              |
| config         | object                 | The optional configuration object for the request.                                |
| config.headers | Record<string, string> | Optional headers (key-vaue pairs) to include in the request                       |
| config.timeout | number                 | The timeout in milliseconds (default: 30000). The maximum allowed value is 30000. |

#### Returns

The HTTP response

---

## Availability

### availability.isWithinWorkingHours(handoverId: string): boolean

Checks if a handover instance is within working hours

#### Arguments

| Name       | Type   | Description                       |
| ---------- | ------ | --------------------------------- |
| handoverId | string | The handover instance ID to check |

#### Returns

true if within working hours, false otherwise

---

## API for Orders Integration

### integrations.orders.searchByOrderNumber(orderNumber: string): Order[]

Searches for orders by order number across all integrations.

#### Arguments

| Name        | Type   | Description                     |
| ----------- | ------ | ------------------------------- |
| orderNumber | string | The order number to search for. |

#### Returns

An array of orders matching the order number.

### integrations.orders.searchByOrderNumber(orderNumber: string, integrationIds: string[]): Order[]

Searches for orders by order number in specific integrations.

#### Arguments

| Name           | Type     | Description                           |
| -------------- | -------- | ------------------------------------- |
| orderNumber    | string   | The order number to search for.       |
| integrationIds | string[] | The integration IDs to search within. |

#### Returns

An array of orders matching the order number.

### integrations.orders.searchByEmail(email: string): Order[]

Searches for orders by email across all integrations.

#### Arguments

| Name  | Type   | Description              |
| ----- | ------ | ------------------------ |
| email | string | The email to search for. |

#### Returns

An array of orders matching the email.

### integrations.orders.searchByEmail(email: string, integrationIds: string[]): Order[]

Searches for orders by email in specific integrations.

#### Arguments

| Name           | Type     | Description                           |
| -------------- | -------- | ------------------------------------- |
| email          | string   | The email to search for.              |
| integrationIds | string[] | The integration IDs to search within. |

#### Returns

An array of orders matching the email.

### integrations.orders.searchByPhoneNumber(phoneNumber: string): Order[]

Searches for orders by phone number across all integrations.

#### Arguments

| Name        | Type   | Description                     |
| ----------- | ------ | ------------------------------- |
| phoneNumber | string | The phone number to search for. |

#### Returns

An array of orders matching the phone number.

### integrations.orders.searchByPhoneNumber(phoneNumber: string, integrationIds: string[]): Order[]

Searches for orders by phone number in specific integrations.

#### Arguments

| Name           | Type     | Description                           |
| -------------- | -------- | ------------------------------------- |
| phoneNumber    | string   | The phone number to search for.       |
| integrationIds | string[] | The integration IDs to search within. |

#### Returns

An array of orders matching the phone number.

### integrations.orders.get(orderId: string, integrationId: string): Order \| null

Gets an order by ID from a specific integration.

#### Arguments

| Name          | Type   | Description                               |
| ------------- | ------ | ----------------------------------------- |
| orderId       | string | The order ID to get.                      |
| integrationId | string | The integration ID to get the order from. |

#### Returns

The order information or null if no order is found.

### integrations.orders.cancel(orderId: string, integrationId: string, refund: RefundConfig): IntegrationResponse

Cancels an order in a specific integration.

#### Arguments

| Name          | Type         | Description                                  |
| ------------- | ------------ | -------------------------------------------- |
| orderId       | string       | The order ID to cancel.                      |
| integrationId | string       | The integration ID to cancel the order from. |
| refund        | RefundConfig | The refund configuration.                    |

#### Returns

A response object with the outcome and value/reason.

### integrations.orders.refund(orderId: string, integrationId: string, refund: RefundConfig): IntegrationResponse

Refunds an order in a specific integration.

#### Arguments

| Name          | Type         | Description                                  |
| ------------- | ------------ | -------------------------------------------- |
| orderId       | string       | The order ID to refund.                      |
| integrationId | string       | The integration ID to refund the order from. |
| refund        | RefundConfig | The refund configuration.                    |

#### Returns

A response object with the outcome and value/reason.

### integrations.orders.updateShippingAddress(orderId: string, integrationId: string, address: UpdateAddress): IntegrationResponse

Updates the shipping address of an order in a specific integration.

#### Arguments

| Name          | Type          | Description                                  |
| ------------- | ------------- | -------------------------------------------- |
| orderId       | string        | The order ID to update.                      |
| integrationId | string        | The integration ID to update the order from. |
| address       | UpdateAddress | The new shipping address.                    |

#### Returns

A response object with the outcome and value/reason.

### integrations.orders.updatePhoneNumber(orderId: string, integrationId: string, phoneNumber: string): IntegrationResponse

Updates the phone number of an order in a specific integration.

#### Arguments

| Name          | Type   | Description                                  |
| ------------- | ------ | -------------------------------------------- |
| orderId       | string | The order ID to update.                      |
| integrationId | string | The integration ID to update the order from. |
| phoneNumber   | string | The new phone number.                        |

#### Returns

A response object with the outcome and value/reason.

### integrations.orders.updateEmail(orderId: string, integrationId: string, email: string): IntegrationResponse

Updates the email of an order in a specific integration.

#### Arguments

| Name          | Type   | Description                                  |
| ------------- | ------ | -------------------------------------------- |
| orderId       | string | The order ID to update.                      |
| integrationId | string | The integration ID to update the order from. |
| email         | string | The new email.                               |

#### Returns

A response object with the outcome and value/reason.

### integrations.orders.addNote(orderId: string, integrationId: string, note: string): IntegrationResponse

Adds a note to an order in a specific integration.

#### Arguments

| Name          | Type   | Description                                  |
| ------------- | ------ | -------------------------------------------- |
| orderId       | string | The order ID to update.                      |
| integrationId | string | The integration ID to update the order from. |
| note          | string | The note to add.                             |

#### Returns

A response object with the outcome and value/reason.

### integrations.orders.addTags(orderId: string, integrationId: string, tags: string[]): IntegrationResponse

Adds tags to an order in a specific integration.

#### Arguments

| Name          | Type     | Description                                  |
| ------------- | -------- | -------------------------------------------- |
| orderId       | string   | The order ID to update.                      |
| integrationId | string   | The integration ID to update the order from. |
| tags          | string[] | The tags to add.                             |

#### Returns

A response object with the outcome and value/reason.

## API for Products Integration

### integrations.products.search(options: ProductCatalogueSearchOptions): CatalogueProduct[]

Searches for products in a specific integration.

#### Arguments

| Name    | Type                          | Description                 |
| ------- | ----------------------------- | --------------------------- |
| options | ProductCatalogueSearchOptions | The options for the search. |

#### Returns

The products or null if no products are found.

## API for Returns Integration

### integrations.returns.searchByEmail(email: string): ReturnDetails[]

Searches for returns by customer email across all integrations.

#### Arguments

| Name  | Type   | Description              |
| ----- | ------ | ------------------------ |
| email | string | The email to search for. |

#### Returns

An array of returns matching the email.

### integrations.returns.searchByEmail(email: string, integrationIds: string[]): ReturnDetails[]

Searches for returns by customer email in specific integrations.

#### Arguments

| Name           | Type     | Description                           |
| -------------- | -------- | ------------------------------------- |
| email          | string   | The email to search for.              |
| integrationIds | string[] | The integration IDs to search within. |

#### Returns

An array of returns matching the email.

### integrations.returns.process(returnId: string, integrationId: string): IntegrationResponse

Processes a return in a specific integration.

#### Arguments

| Name          | Type   | Description                                    |
| ------------- | ------ | ---------------------------------------------- |
| returnId      | string | The return ID to process.                      |
| integrationId | string | The integration ID to process the return from. |

#### Returns

A response object with the outcome and value/reason.

### integrations.returns.cancel(returnId: string, integrationId: string): IntegrationResponse

Cancels a return in a specific integration.

#### Arguments

| Name          | Type   | Description                                   |
| ------------- | ------ | --------------------------------------------- |
| returnId      | string | The return ID to cancel.                      |
| integrationId | string | The integration ID to cancel the return from. |

#### Returns

A response object with the outcome and value/reason.

### integrations.returns.close(returnId: string, integrationId: string): IntegrationResponse

Closes a return in a specific integration.

#### Arguments

| Name          | Type   | Description                                  |
| ------------- | ------ | -------------------------------------------- |
| returnId      | string | The return ID to close.                      |
| integrationId | string | The integration ID to close the return from. |

#### Returns

A response object with the outcome and value/reason.

### integrations.returns.flag(returnId: string, integrationId: string): IntegrationResponse

Flags a return in a specific integration.

#### Arguments

| Name          | Type   | Description                                 |
| ------------- | ------ | ------------------------------------------- |
| returnId      | string | The return ID to flag.                      |
| integrationId | string | The integration ID to flag the return from. |

#### Returns

A response object with the outcome and value/reason.

### integrations.returns.createReturnLink(orderId: string, orderIntegrationId: string): IntegrationResponse

Creates a return link for a provided order.

#### Arguments

| Name               | Type   | Description                      |
| ------------------ | ------ | -------------------------------- |
| orderId            | string | The ID of an order.              |
| orderIntegrationId | string | The integration ID for an order. |

#### Returns

A result for create return link action.

## API for Subscriptions Integration

### integrations.subscriptions.searchByEmail(email: string): SubscriptionDetails[]

Searches for subscriptions by customer email across all integrations.

#### Arguments

| Name  | Type   | Description              |
| ----- | ------ | ------------------------ |
| email | string | The email to search for. |

#### Returns

An array of subscriptions matching the email.

### integrations.subscriptions.searchByEmail(email: string, integrationIds: string[]): SubscriptionDetails[]

Searches for subscriptions by customer email in specific integrations.

#### Arguments

| Name           | Type     | Description                           |
| -------------- | -------- | ------------------------------------- |
| email          | string   | The email to search for.              |
| integrationIds | string[] | The integration IDs to search within. |

#### Returns

An array of subscriptions matching the email.

### integrations.subscriptions.cancel( subscriptionId: string, integrationId: string, sendEmail: boolean, cancellationReason: string, cancellationReasonComments?: string ): IntegrationResponse

Cancels a subscription in a specific integration.

#### Arguments

| Name                       | Type    | Description                                            |
| -------------------------- | ------- | ------------------------------------------------------ |
| subscriptionId             | string  | The subscription ID to cancel.                         |
| integrationId              | string  | The integration ID to cancel the subscription from.    |
| sendEmail                  | boolean | Whether to send an email notification to the customer. |
| cancellationReason         | string  | The reason for cancellation.                           |
| cancellationReasonComments | string  | Optional comments for the cancellation reason.         |

#### Returns

A response object with the outcome and value/reason.

### integrations.subscriptions.reschedule( subscriptionId: string, integrationId: string, nextChargeAt: number ): IntegrationResponse

Reschedules a subscription in a specific integration.

#### Arguments

| Name           | Type   | Description                                             |
| -------------- | ------ | ------------------------------------------------------- |
| subscriptionId | string | The subscription ID to reschedule.                      |
| integrationId  | string | The integration ID to reschedule the subscription from. |
| nextChargeAt   | number | The timestamp for the next charge in milliseconds.      |

#### Returns

A response object with the outcome and value/reason.

## API for Ticketing Integration

### integrations.tickets.create( integrationId: string, subject: string, content: string, isHtmlContent: boolean, note: string, requester: RequesterInfo, tags: string[], fields: CustomField[], zendeskExtraProperties?: ZendeskTicketExtraProperties ): IntegrationResponse

Creates a new ticket in a specific integration.

#### Arguments

| Name                   | Type                         | Description                                                           |
| ---------------------- | ---------------------------- | --------------------------------------------------------------------- |
| integrationId          | string                       | The integration ID to create the ticket in.                           |
| subject                | string                       | The subject of the ticket.                                            |
| content                | string                       | The content of the ticket.                                            |
| isHtmlContent          | boolean                      | Whether the content is HTML.                                          |
| note                   | string                       | An optional note for the ticket. Leave as empty string if not needed. |
| requester              | RequesterInfo                | Information about the requester.                                      |
| tags                   | string[]                     | Tags to add to the ticket.                                            |
| fields                 | CustomField[]                | Custom fields for the ticket.                                         |
| zendeskExtraProperties | ZendeskTicketExtraProperties | Optional extra properties for Zendesk tickets.                        |

#### Returns

A response object with the outcome and value/reason.

# Code Block Data Types

## Message

Represents a message in the interaction

### Properties

| Name       | Type                | Description                             |
| ---------- | ------------------- | --------------------------------------- |
| author     | "User" \| "Chatbot" | The author of the message               |
| content    | string              | The content of the message              |
| timeMillis | number              | The time of the message in milliseconds |

---

## IntentResult

Represents the intent result

### Properties

| Name       | Type   | Description          |
| ---------- | ------ | -------------------- |
| id         | string | The intent ID        |
| name       | string | The intent name      |
| confidence | number | The confidence level |

---

## User

Represents the user information

### Properties

| Name        | Type           | Description                                          |
| ----------- | -------------- | ---------------------------------------------------- |
| userId      | string         | The user ID                                          |
| email       | string \| null | The email of the user or null if not provided        |
| phoneNumber | string \| null | The phone number of the user or null if not provided |
| platformId  | string         | The platform ID                                      |
| language    | string         | The language of the user                             |

---

## CrmUser

Represents the user information available through CRM

### Properties

| Name          | Type           | Description                                          |
| ------------- | -------------- | ---------------------------------------------------- |
| name          | string \| null | The name of the user or null if not provided         |
| firstName     | string \| null | The first name of the user or null if not provided   |
| lastName      | string \| null | The last name of the user or null if not provided    |
| phoneNumber   | string \| null | The phone number of the user or null if not provided |
| email         | string \| null | The email of the user or null if not provided        |
| locale        | string \| null | The locale of the user or null if not provided       |
| language      | string \| null | The language of the user or null if not provided     |
| timeZone      | string \| null | The time zone of the user or null if not provided    |
| authenticated | string \| null | The authentication status or null if not provided    |
| accessToken   | string \| null | The access token or null if not provided             |
| [key: string] | string         | Custom properties can be added with string keys      |

---

## HttpResponse

Represents the HTTP response

### Properties

| Name    | Type                   | Description                                                                                                                                                           |
| ------- | ---------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| outcome | "success" \| "failure" | The outcome of the response, either "success" or "failure"                                                                                                            |
| status  | number                 | The status code of the response (optional)                                                                                                                            |
| body    | object \| string       | The body of the response. Either an object (parsed JSON) when backend responds with ContentType: application/json or a string when ContentType: text/plain (optional) |
| error   | string                 | The error message in case of a connection error (optional)                                                                                                            |

---

## PriceSummary

Represents a price summary for an order

### Properties

| Name     | Type   | Description               |
| -------- | ------ | ------------------------- |
| currency | string | The currency of the price |
| subtotal | number | The subtotal amount       |
| discount | number | The discount amount       |
| shipping | number | The shipping amount       |
| tax      | number | The tax amount            |
| total    | number | The total amount          |

---

## LineItem

Represents a line item in an order

### Properties

| Name             | Type            | Description                           |
| ---------------- | --------------- | ------------------------------------- |
| id               | string          | The ID of the line item               |
| productId        | string          | The product ID                        |
| variantId        | string          | The variant ID                        |
| title            | string          | The title of the product              |
| description      | string \| null  | The description of the product        |
| price            | number          | The price of the product              |
| currency         | string          | The currency of the price             |
| quantity         | number          | The quantity ordered                  |
| shopUrl          | string \| null  | The shop URL                          |
| imageUrl         | string \| null  | The image URL                         |
| sku              | string \| null  | The SKU                               |
| requiresShipping | boolean \| null | Whether physical shipping is required |

---

## Fulfillment

Represents a fulfillment for an order

### Properties

| Name                      | Type           | Description                                 |
| ------------------------- | -------------- | ------------------------------------------- |
| id                        | string         | The ID of the fulfillment                   |
| createdAtMillis           | number \| null | The creation time in milliseconds           |
| deliveryProvider          | string \| null | The delivery provider                       |
| status                    | string \| null | The status of the fulfillment               |
| trackingNumber            | string \| null | The tracking number                         |
| trackingUrl               | string \| null | The tracking URL                            |
| estimatedDeliveryAtMillis | number \| null | The estimated delivery time in milliseconds |
| deliveredAtMillis         | number \| null | The actual delivery time in milliseconds    |

---

## Address

Represents an address

### Properties

| Name         | Type           | Description                          |
| ------------ | -------------- | ------------------------------------ |
| name         | string \| null | The name associated with the address |
| addressLine1 | string \| null | The first line of the address        |
| addressLine2 | string \| null | The second line of the address       |
| zip          | string \| null | The ZIP/postal code                  |
| city         | string \| null | The city                             |
| province     | string \| null | The province/state                   |
| country      | string \| null | The country                          |
| provinceCode | string \| null | The province/state code              |
| countryCode  | string \| null | The country code                     |

---

## UpdateAddress

Represents an address with required fields

### Properties

| Name         | Type           | Description                          |
| ------------ | -------------- | ------------------------------------ |
| name         | string         | The name associated with the address |
| addressLine1 | string         | The first line of the address        |
| addressLine2 | string \| null | The second line of the address       |
| zip          | string         | The ZIP/postal code                  |
| city         | string         | The city                             |
| province     | string \| null | The province/state                   |
| country      | string         | The country                          |
| provinceCode | string \| null | The province/state code              |
| countryCode  | string \| null | The country code                     |

---

## DeliveryMethod

Represents a delivery method

### Properties

| Name         | Type           | Description                     |
| ------------ | -------------- | ------------------------------- |
| name         | string         | The name of the delivery method |
| providerName | string \| null | The provider name               |
| providerCode | string \| null | The provider code               |

---

## ContactDetails

Represents contact details

### Properties

| Name        | Type           | Description       |
| ----------- | -------------- | ----------------- |
| email       | string \| null | The email address |
| phoneNumber | string \| null | The phone number  |

---

## OrderCustomProperty

Represents a custom property for an order

### Properties

| Name  | Type   | Description               |
| ----- | ------ | ------------------------- |
| key   | string | The key of the property   |
| label | string | The label of the property |
| value | string | The value of the property |

---

## Order

Represents data of an order

### Properties

| Name              | Type                   | Description                             |
| ----------------- | ---------------------- | --------------------------------------- |
| orderId           | string                 | The unique identifier of the order      |
| orderNumber       | string                 | The order number                        |
| status            | string                 | The status of the order                 |
| createdAt         | number                 | The creation time in milliseconds       |
| priceSummary      | PriceSummary           | The price summary of the order          |
| lineItems         | LineItem[]             | The line items in the order             |
| fulfillments      | Fulfillment[]          | The fulfillments for the order          |
| billingAddress    | Address \| null        | The billing address                     |
| shippingAddress   | Address \| null        | The shipping address                    |
| tags              | string[]               | The tags associated with the order      |
| adminUrl          | string \| null         | The admin URL for the order             |
| storeUrl          | string \| null         | The store URL for the order             |
| financialStatus   | string \| null         | The financial status of the order       |
| fulfillmentStatus | string \| null         | The fulfillmentment status of the order |
| deliveryMethods   | DeliveryMethod[]       | The delivery methods for the order      |
| contactDetails    | ContactDetails \| null | The contact details for the order       |
| processedAt       | number \| null         | The processing time in milliseconds     |
| customProperties  | OrderCustomProperty[]  | The custom properties for the order     |
| integrationId     | string \| null         |                                         |

---

## CatalogueProductVariant

Represents a variant of a product in the catalogue

### Properties

| Name             | Type            | Description                           |
| ---------------- | --------------- | ------------------------------------- |
| variantId        | string          | The unique identifier of the variant  |
| title            | string          | The title of the variant              |
| minPrice         | number          | The minimum price of the variant      |
| maxPrice         | number          | The maximum price of the variant      |
| imageUrl         | string \| null  | The image URL                         |
| sku              | string \| null  | The SKU                               |
| requiresShipping | boolean \| null | Whether physical shipping is required |

---

## CatalogueProduct

Represents a product in the catalogue

### Properties

| Name      | Type                      | Description                              |
| --------- | ------------------------- | ---------------------------------------- |
| productId | string                    | The unique identifier of the product     |
| title     | string                    | The title of the product                 |
| shopUrl   | string                    | The shop URL                             |
| imageUrl  | string \| null            | The image URL                            |
| tags      | string[]                  | The tags associated with the product     |
| skus      | string[]                  | The SKUs associated with the product     |
| variants  | CatalogueProductVariant[] | The variants associated with the product |

---

## RefundConfig

Represents a refund configuration for an order

### Properties

| Name               | Type                                                                                       | Description                                                      |
| ------------------ | ------------------------------------------------------------------------------------------ | ---------------------------------------------------------------- |
| currency           | string                                                                                     | The currency of the refund                                       |
| reason             | "RESTOCK" \| "DAMAGED" \| "CUSTOMER" \| "OTHER"                                            | The reason for the refund                                        |
| notifyCustomer     | boolean                                                                                    | Whether to notify the customer about the refund (default: false) |
| note               | string                                                                                     | Optional note for the refund                                     |
| refundLineItems    | { itemId: string; quantity: number; restockType: "CANCEL" \| "RETURN" \| "NO_RESTOCK"; }[] | Line items to be refunded (default: [])                          |
| refundCustomAmount | number                                                                                     | Optional custom amount to refund                                 |
| refundShipping     | number                                                                                     | Optional shipping refund                                         |

---

## ProductCatalogueSearchOptions

Represents options for searching products in the catalogue

### Properties

| Name           | Type     | Description                                               |
| -------------- | -------- | --------------------------------------------------------- |
| integrationId  | string   | The integration ID to limit the search to                 |
| query          | string   | The query to search for                                   |
| tags           | string[] | The tags to search within                                 |
| page           | number   | The page number to search on (default: 1)                 |
| entriesPerPage | number   | The number of entries per page to search on (default: 20) |

---

## ReturnItem

Represents a return item

### Properties

| Name             | Type           | Description                          |
| ---------------- | -------------- | ------------------------------------ |
| id               | string         | The ID of the return item            |
| name             | string         | The name of the item                 |
| sku              | string \| null | The SKU of the item                  |
| quantity         | number         | The quantity returned                |
| price            | number         | The price of the item                |
| currency         | string         | The currency of the price            |
| shopUrl          | string \| null | The shop URL for the item            |
| imageUrl         | string \| null | The image URL for the item           |
| reasonType       | string \| null | The reason type for the return       |
| reasonName       | string \| null | The reason name for the return       |
| compensationType | string \| null | The compensation type for the return |

---

## ReturnShipping

Represents shipping details for a return

### Properties

| Name           | Type           | Description              |
| -------------- | -------------- | ------------------------ |
| trackingNumber | string \| null | The tracking number      |
| trackingUrl    | string \| null | The tracking URL         |
| carrier        | string \| null | The carrier name         |
| method         | string \| null | The shipping method      |
| cost           | number \| null | The shipping cost        |
| currency       | string \| null | The currency of the cost |

---

## ReturnDetails

Represents details of a return

### Properties

| Name          | Type                   | Description                                 |
| ------------- | ---------------------- | ------------------------------------------- |
| returnId      | string                 | The unique identifier of the return         |
| statusType    | string                 | The status type of the return               |
| statusName    | string                 | The status name of the return               |
| orderNumber   | string                 | The order number associated with the return |
| items         | ReturnItem[]           | The items in the return                     |
| shipping      | ReturnShipping \| null | The shipping details for the return         |
| currency      | string                 | The currency of the return                  |
| totalAmount   | number                 | The total amount of the return              |
| adminUrl      | string \| null         | The admin URL for the return                |
| portalUrl     | string \| null         | The portal URL for the return               |
| integrationId | string                 | The integration ID for the return           |

---

## SubscriptionDetails

Represents details of a subscription

### Properties

| Name               | Type            | Description                                          |
| ------------------ | --------------- | ---------------------------------------------------- |
| subscriptionId     | string          | The unique identifier of the subscription            |
| status             | string          | The status of the subscription                       |
| title              | string          | The title of the subscription                        |
| createdAt          | number          | The creation time in milliseconds                    |
| cancelledAt        | number \| null  | The cancellation time in milliseconds (if cancelled) |
| cancellationReason | string \| null  | The reason for cancellation (if cancelled)           |
| price              | number          | The price of the subscription                        |
| quantity           | number          | The quantity of the subscription                     |
| currency           | string          | The currency of the subscription                     |
| firstChargeAt      | number \| null  | The time of the first charge in milliseconds         |
| lastChargeAt       | number \| null  | The time of the last charge in milliseconds          |
| nextChargeAt       | number \| null  | The time of the next charge in milliseconds          |
| adminUrl           | string \| null  | The admin URL for the subscription                   |
| integrationId      | string \| null  | The integration ID for the subscription              |
| shippingAddress    | Address \| null | The shipping address                                 |


---

## RequesterInfo

Represents information about the requester for a ticket

### Properties

| Name  | Type   | Description                                  |
| ----- | ------ | -------------------------------------------- |
| email | string | The email of the requester                   |
| name  | string | The name of the requester (optional)         |
| phone | string | The phone number of the requester (optional) |

---

## CustomField

Represents a custom field for a ticket

### Properties

| Name  | Type   | Description                   |
| ----- | ------ | ----------------------------- |
| key   | string | The key of the custom field   |
| value | string | The value of the custom field |

---

## ZendeskTicketExtraProperties

Represents extra properties for a Zendesk ticket

### Properties

| Name      | Type     | Description                   |
| --------- | -------- | ----------------------------- |
| brandId   | number   | The brand ID (optional)       |
| productId | number   | The product ID (optional)     |
| ccEmails  | string[] | CC email addresses (optional) |

---

## IntegrationResponse

Represents a response from an integration operation

### Properties

| Name    | Type                   | Description                                                                       |
| ------- | ---------------------- | --------------------------------------------------------------------------------- |
| outcome | "success" \| "failure" | The outcome of the operation, either "success" or "failure"                       |
| value   | string                 | The value returned if the operation was successful (usually the ID of the entity) |
| reason  | string                 | The reason for failure if the operation failed (optional)                         |

---

## CarouselElement

### Properties

| Name          | Type   | Description |
| ------------- | ------ | ----------- |
| title         | string |             |
| subtitle      | string |             |
| imageUrl      | string |             |
| buttonUrl     | string |             |
| buttonCaption | string |             |
