# ManaFlair
ManaFlair Decentraland Avatar Aura System

## Concept
User clicks a button entity (a cube button with words 'Load ManaFlair Aura') in the scene.

User address is read from browser, checked if exists in Lemursiv Aura Database in node mongodb (server code from skr-v/PixelArtDCL/server/)

If not existing then ADD new user username (eth public address) to the database.
User can then attach entities from the scene to their avatar.  Code here - Attach an entity to the player: https://docs.decentraland.org/development-guide/entity-positioning/#attach-an-entity-to-the-player  using the Attachable.PLAYER type.
When an entity is attached, add that entity name to the Database user also. For example, Coffee, Matcha, Yerba Mate. Use example.glb models for now.
IF a username already has an account in the database then attach the entities to their avatar.  New copies of entities may need to be loaded.

Code snippets below.

////Get eth address example code is here.
/////ETH addres read on button press to accept.

var ethAddress = "anon"

import { getUserAccount } from '@decentraland/EthereumController'
     //   getETHAddress()
  function getETHAddress()
  {
    executeTask(async () => {
      try {
        const address = await getUserAccount()
        //log("Got address " + address)
        ethAddress = address
//log("Got eth address " + ethAddress + "got address " + address)
       //ADD CODE HERE TO POST
      } catch (error) {
        log(error.toString())
        ethAddress = "guest"
        station1.updatePlayerAddress(ethAddress)
       
      }
    })
  
  }

//example code to post the data to the server (this.station refers to server URL)
  let url = `${this.station]}/api/manaflairs/color`
  let method = 'POST'
  let headers = { 'Content-Type': 'application/json' }
  let body = JSON.stringify({ color: color, address:this.playerAddress })
 // log('body logged as ' + body)
  executeTask(async () => {
    try {
      let response = await fetch(url, {
        headers: headers,
        method: method,
        body: body
      })
    } catch {
      log('error sending Aura change')
    }
  })

