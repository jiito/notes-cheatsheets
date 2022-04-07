# Working with Global State in React 
Problem: I have a service that I am initiating in a class Service. I have made a  #get() method for that service to provide the instance saved on the class. 

I want all parts of the app to share the same instance. 

I believe I am currently running into a race condition where two calls to the custom hook are requesting and instance before the first call has finished the async creation option.  

## questions: 
1. does it make sense for this logic to be done on the backend? i.e. we send a pairing request to to our own internal APIs and then that send's a response. The event listeners would then we attached on the server. 
   1. This would make it harder to send updates to the front-end about events. I.e. if the user needs to sign a request, we would have to get the event from the backend which doesn't make sense 


## Current approach 
I am currently using a hook to try and get the instance from the Service class. This seems redundant. # Working with Global State in React 
Problem: I have a service that I am initiating in a class Service. I have made a  #get() method for that service to provide the instance saved on the class. 

I want all parts of the app to share the same instance. 