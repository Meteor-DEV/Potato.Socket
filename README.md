# Potato.Socket
##### Your internet is fast as Potato? 
##### Use (R)Potato.Socket(tm)
## WTF is this?!
Potato socket - is a WebSocket wrapper with built-in serialization/deserialization support backed by ProtoDef


## Usage:
### Client:
```js
import {createPotatoSocket} from 'potato.socket';

// Wrap websocket
const socket=createPotatoSocket(new WebSocket('wss://domain.with.potato/socketUrl'));

// Add all needed packets
potato.addPacket('test',{
    a:'string'     
});

// Finish packet declaration, starts ProtoDef parser
potato.finishDeclaration();

// Add your listeners (Make sure you defined packet "test"!)
potato.on('test',(a)=>{
    console.log(a);
});

// And RPC methods!
potato.testClientMethod=(data)=>{
    return ++data;
}

// Emit data to server (Make sure you defined packet "test"!)
potato.emit('test',{
    a:'123412124'
});
await potato.testServerMethod(5); // 4
```
### Server:
```js
import XPress from '@meteor-it/xpress';
import {addSupport as addPotatoSupport} from '@meteor-it/xpress-support-potato';

const server=new XPress('test');

server.on('POTATO /socketUrl',(req,potato)=>{
    // Add all needed packets
    potato.addPacket('test',{
        a:'string'     
    });
    
    // Finish packet declaration, starts ProtoDef parser
    potato.finishDeclaration();
    
    // Add your listeners (Make sure you defined packet "test"!)
    potato.on('test',(a)=>{
        console.log(a);
    });
    
    // And RPC methods!
    potato.testServerMethod=(data)=>{
        return --data;
    }
    
    // Emit data to client (Make sure you defined packet "test"!)
    potato.emit('test',{
        a:'123412124'
    });
    
    await potato.testClientMethod(5); // 6
});
```