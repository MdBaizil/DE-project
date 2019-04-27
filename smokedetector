// Code references : https://github.com/netsec-ethz/scion-homeworks/blob/master/latency/timestamp_client.go and reference https://github.com/perrig/scionlab/blob/master/sensorapp/sensorfetcher/sensorfetcher.go

package main



import (

	"flag"

	"fmt"  //importing fmt package for printing

	"log"

	"github.com/scionproto/scion/go/lib/snet" //importing snet packages for the scion connections

	"github.com/scionproto/scion/go/lib/sciond"
	"github.com/davecheney/gpio"
	

)


func geterror(e error) {   //Error function



if e!=nil{
log.Println(e)

}

}


func main() {
	pin, err := gpio.OpenPin(gpio.GPIO18, gpio.ModeInput)
	if err != nil{
		fmt.Printf("error opening pin %s\n",err)
	return
	}
	go func(){
				var ( // necessary variable declarations

				 message string

				 clientadd string

				 serveradd string
				 
				 e error

				 //client *snet.Addr

				 server *snet.Addr

				 udpConnection  *snet.Conn
				)

				flag.StringVar(&clientadd, "c", "", "address of client") // fetch address values from command line

				flag.StringVar(&serveradd, "s", "", "address of server")// fetch server address from command line

				flag.Parse()


				//client, e = snet.AddrFromString(clientadd)  // AddrFromString converts an address string of format isd-as,[ipaddr]:port


				geterror(e)

				server, e = snet.AddrFromString(serveradd)

				geterror(e)

				daddr := "/run/shm/dispatcher/default.sock"


		        snet.Init(server.IA, sciond.GetDefaultSCIONDPath(nil), daddr) //initialises scion network


				udpConnection, e = snet.ListenSCION("udp4", server) // client connects to server through UDP

				geterror(e)
				//packetsent := make([]byte, 3000)

				for {

					message = "smoke detected"

					_, e = udpConnection.Write([]byte(message)) //sending message to server
					geterror(e)

				}
}()

err = pin.BeginWatch(gpio.EdgeFalling, func(){
	fmt.Printf("smoke detection test\n",gpio.GPIO18)
})

}
