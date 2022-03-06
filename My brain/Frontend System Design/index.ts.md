# First Things First
1. General Requeirments
2.  Requirements
3. Components Architecture
4. Data Entities
5. Data API 
6. Data Store
7. Optimization
8. Accessibilty

## General Requierments
What are the things that user can do? 

## Components Architecture
This is where you define all the features of the app.

Inside a graph, you start with the Big components inside your app, then goes down the tree, mentioning all the small components/features

![[Pasted image 20220218162125.png]]

*Another example here from Data Table Compoenent*
![[Pasted image 20220219133403.png]]
Here Data Table Compoenent Table is at the top, then we break it down into small components


## Data API 
If its anything to do with real-time data then you'll have three options

### Long Polling
Very simple request that you make after some interval of time.

**Pros**
- HTTP Benefits
- Very Simple to implement
**Cons**
- Latency can be long
- Connections can timeout
- Traffic Overhead, becuase you are sending a lot of data like headers and stuff. 

### Web Sockets

**Pros**
- Duplex Communication i.e Server can send us messages and we can send the server some messages
- They are super fast as they work on TCP connection, so latency is very low
**Cons**
- Keeping a web socket connection is pretty resource heavy and expensive
- not HTTP2 compatible, HTTP2 gives a lot of performance benefits

### Server-Sent Events (SSE)

**Pros**
- HTTP2 benefits (caching and asset zipping) and it is also compatible with HTTP2
- It gives only what we need in text format
-  SSE does'nt waste resources , very resource efficient
- does not have any traffic overhead
**Cons**
- Its Unidirectional. We can get data from server but we can't send data back to server
- It only sends Text Data



 **After you select the Mode of API you are going to use**

 Make the basic level schema and try to connect everything according to the component Architecture
 ![[Pasted image 20220218175043.png]]


## Frontend Data store

![[Pasted image 20220218175537.png]]

According to the schema you just made, make the schema for the data store in frontend and normalize it in a way so that its not very nested and easy to access. 

Basically just store the data how the schema is.

## Optimization

**Network Performance**

1. Gzip
2. brotli compression for bundle size
3. Webp image format and png format as fallback when webp is not supported. 
4. Using HTTP2 for bundle splitting

**Rendering Perfomance**

1. Inline critical Resources
2. non-critical Resources must be used in defer mode
3. To avoid reflows uss css animations
4. Show Skeleton When loading data from network
**When you want to render a lot of dom elements** Then you have to maintain constant number of nodes with **virtualization**

**JS Performance**

1. Do async stuff and do less stuff in general
2. If there is a expensive task that needs to be done in client side then do it in a web worker
3. Do not **Block the UI Thread**, as this can be done pretty easily if we try to filter a large amount of data. We can move this filter function a web worker instead, so that we dont block thread or we can run the filter function server side.
4. Use [Event Delegation](obsidian://open?vault=MyVault&file=My%20brain%2FJavascript%20Course%20files%2FEvents) Whenever there is a huge list and you want to find out exactly which item or element was clicked. Just attach some attribute to these items so that you can get it with javascript

## Accessibility

1. Use `rem` unit in css to respect the browser setting of a user like zoom and font sizes
2. Try to give hotkeys for things that happen the most in your app
3. Give more color schemes options for people with color blindness
4. Announce all live fields with `aria-live` for people with blindness
5. All images should have correct alt attribute
6.  Use all the correct tags for HTML5

## Consistency 
1. Browsers can be diffrent but our app should be looking similar in styleson every platform. so we use some css properties perfixes and pollyfills to manitain that
2. Having a design system for centralized design guidelines, so that anyone consuming it have the same styles 

## Logging and Monitoring
1. Setup a Error Logging service (sentry)
2. User tracking
3. User activity
4. Feature usage logging

## Database and Caching
Caching data that came from network request so that it can rendered quickly. and only requesting data when its needed.

## Testing

1. Unit testing - Testing every littile functions and components
2. Integration Testing - testing combination of testing
3. End to End testing - E2E testing to test the whole flow of the app