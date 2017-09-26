# 0kelvin
Machine Framework for 0kelvin - the coldest private key storage

Open Framework ToDo Overview (All of these modules will be added to this repository as they are developed)

CAD files
- 0kelvin brick design
- Manufacturing instructions
- Materials list

Web-App
- Split key generation
- Vanity address generation
- Spending instructions
- Password protected brick integration

--

0kelvin Machine Framework Detail: Web-App
The 0kelvin machine framework is a completely open-source design and application to allow the easy creation of secure storage bricks. Optionally, the party generating the brick for you has no access to the private key, only the public key. 

Part of the framework will include a web-app that generates a split key according to a brainwallet (password) scheme, or even a Vanity address. From the user-side, it will be very simple, but it works like this and can be done manually:
1. You create a random 256-bit integer less than the SECP256k1 generator. You keep this secret. (Effectively, an ECDSA private key.)
2. You compute the corresponding EC point on the SECP256k1 curve. You share this with whoever is creating the 0kelvin brick for you. (This is the ECDSA public key that corresponds to the private key you generated in step one.)
3. The party generating the brick tries various 256-bit integers also less than the generator. They compute the corresponding EC point and add it to the EC point you sent them (from step two). They then hash this and see if it produces the desired vanity address. They repeat this over and over until they find a 256-bit integer that works. They give this integer to you. (And the world, it need not be kept secret.)
4. You add the 256-bit integer they found to the 256-bit integer you generated in step 1 and reduce it modulo the SECP256k1 generator.
5. You now have the private key, and they don’t. (And you can prove that they cannot generate the private key from just the information you gave them unless ECDSA is fundamentally broken.)
