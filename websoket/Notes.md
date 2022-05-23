# WEB SOCKETS
Web socket is a communication protocol which provides full-duplex communication channels over a single TCP connection.

Web sockets work on two different things which is a an "event emitter" and a "event listener".

There are various libraries available for implementing a web socket in an application. One of them is Socket IO. It primarily uses web socket protocol with polling as a fallback option. It also provides more features like broadcasting to multiple sockets and asynchronous I/O.

## Installation
We can install socket I/O npm package via the following command
````
npm i socket.io-client
````
or 
````
yarn add socket.io-client
````

## Usage
We can create a connection between the server and the client. So, in order to do that we use the following procedure -
````
var socket = io.connect("http://localhost:3000");
````
The above statement creates a open connection between the client and the back end server (http://localhost) running on port 3000.

Socket I/O provides us with an event emitter "emit" function and a event listener "on" function. An example of an event emitter and listener is given below -
````
io.on("connection", (socket) => {
const message = 'connection established';
socket.emit('message', message);
});

io.on("message", (message) => {
console.log("message recieved : ", message);
});
````
The above statement register's an event which listens to whether a connection is established or not. After a connection is established the listener function kicks in, and it emits a message via the emitter function. A new listener handles the emitted event and executes its particular block of code.


# TESTING
Testing is a fundamental process which solidifies the existing code base. It is used for checking the correctness of different working units in a module. There are different types of test like, unit tests, integration tests and end to end tests.
In order to test a particular block of code we follow the most popular way of testing which is referred to as the red-green-refactor cycle. 
In this approach we start with failing tests (red), make the test pass (green), and afterwards clean up and polish the code base (refactor) leaving things in much better shape than when we started.

There are three terminologies following which we write a particular test -
1. Arrange
2. Act
3. Assert(refactor)

## Arrange 
Here we write all the dependencies which we might need for executing the test.

## Act
Here we perform the test

## Assert
After performing the previous two steps we assert and check if the assumed resultant value is retrieved from the executed test. On the basis of the assertion the test either fails or passes.

An example of a unit test is given below - 
````
  test("should display <ActionButton /> component", () => {
	//Arrange
    let actionButton;
    //Act
    const { container } = render(<ActionButton actions={dummyData} />);
    //Assert
    expect(container).toBeInTheDocument();
  });
````

> IMPORTANT : The name of the test should be simple and descriptive enough and we should refrain from putting comments over it. Also, a test should primarily focus on executing and testing a single task.

Sometimes, a component might have a dependency which is required to be mocked. In order to do this, there are some utility functions which are available to us. An example is given below - 

````
jest.mock("axios", () => {
  return {
    create: () => {
      return {
        interceptors: {
          request: { eject: jest.fn(), use: jest.fn() },
          response: { eject: jest.fn(), use: jest.fn() },
        },
        get: () => jest.fn(),
        post: () => jest.fn(),
      };
    },
  };
});
````
This is a mock for "axios". It basically overrides the existing get, post and interceptor functions and returns a mocked response whenever they are invoked during a particular test.

# HIGHER ORDER COMPONENTS
Higher Order Components is a design pattern which focuses on logic re-usability. We can enhance an existing component with some features through this. 
Lets take a scenario where a client asks us to create a button component which increments some value each time we click on it.
````
const button = () => {
const [counter, setCounter] = useState(0);

const incrementCounter = () => {
setCounter(counter+1);
}
return (
<>
<button onClick={incrementCounter}>counter: {counter}</button>
</>
)
}
````

Now, the clients has a different requirement. He wants a header which should increment the value every time the mouse pointer hovers over it.
````
const header = () => {
const [counter, setCounter] = useState(0);
const incrementCounter = () => {
setCounter(counter+1);
}
return (
<>
<h1 onMouseOver={incrementCounter}>counter: {counter}</h1>
</>
)
}
````

If you look closely, we are writing the same logic twice. Now, this is where an HOC (Higher Order Component) comes into the picture. We can create a wrapper component which will include the logic part and we can pass data to the inner component -
````
const HOC = (originalComponent) => {
const NewComponent = () => {
const [counter, setCounter] = useState(0);
const incrementCounter = () => {
setCounter(counter+1);
}
return (
<>
<originalComponent counter={counter} incrementCounter={incrementCounter} />
</>
)
}
return NewComponent; 
}
````
The HOC takes in a component and generates a enhanced component with some new attributes which can be accessed later through props. We can remove the logic part from the button and header components and wrap their exports with HOC.
````
//Import HOC
const button = ({incrementCounter, counter}) => {
return (
<>
<button onClick={incrementCounter}>counter: {counter}</button>
</>
)
}
export default HOC(button);
````
After Wrapping the existing component with the HOC we can access the newer attributes via the props and use it to manipulate the state present in the HOC. This way, we can use the same logic twice for two different components without repeating it.