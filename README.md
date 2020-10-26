# Streams Decoder

## Preparation
Install rust if you don't have it already, find the instructions here https://www.rust-lang.org/tools/install

Make sure you also have the build dependencies installed, if not run:  
`sudo apt install build-essential`  
`sudo apt install pkg-config`  
`sudo apt install libssl-dev`  
`sudo apt update`  


## Installing the Streams Decoder
Download streams_decoder server:  
`git clone https://github.com/iot2tangle/streams-decoder`  
`cd streams-decoder`  
  
Configure the Decoder:  
`nano config.json`  
 
Set the *node* to a high-throughput node to make request response faster. 

  
## Runnig the Server:  
  
Run the Server:  
`cargo run --release`  
This starts the server  

To decode a streams channel call the */decode_channel/<channel_id>* endpoint setting the *channel_id* for example:    
`  
curl --location --request GET 'localhost:8585/decode_channel/64e592476ed7619d04526f6360f150d4bce63046511dde3f8665e5aec6b51ffc0000000000000000:78829daa792010edd2c7dbfb'
`
