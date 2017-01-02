# Orion Labs Onyx BLE GATT audio protocol

## Codec

The Onyx uses the Opus low-latency audio codec for sending audio back and forth.

## Circular buffers

The Onyx uses a series GATT characteristics to act as a form of circular buffers for transmitting and receiving audio.  The microphone on the Onyx has a set of four "notify" type GATT characteristics which will send 20 bytes of Opus formatted audio per characteristic, starting with the first characteristic and running through each to the fourth, then beginning again on the first.  To send audio to the speaker on the Onyx four "write" type characteristics are provided and act in the same manner, writing 20 bytes of Opus formatted audio to these in series will play it back from the speaker.

Microphone buffers:

* f2076886-d8f4-4246-8d81-c6b155e9fc80
* f2076886-d8f4-4246-8d81-c6b155e9fc81
* f2076886-d8f4-4246-8d81-c6b155e9fc82
* f2076886-d8f4-4246-8d81-c6b155e9fc83

Speaker buffers:

* 777445ea-22f0-4254-b206-66aef2ec7540
* 777445ea-22f0-4254-b206-66aef2ec7541
* 777445ea-22f0-4254-b206-66aef2ec7542
* 777445ea-22f0-4254-b206-66aef2ec7543

## Transmitting audio

To transmit audio to the Onyx first set the PTT sink characteristic (0000a115-0000-1000-8000-00805f9b34fb) to `0x01` and start filling the circular buffer with Opus formatted audio (characteristics 777445ea-22f0-4254-b206-66aef2ec7540, 777445ea-22f0-4254-b206-66aef2ec7541, 777445ea-22f0-4254-b206-66aef2ec7542, and 777445ea-22f0-4254-b206-66aef2ec7543).

An example from `gatttool`:

```
[jhe@oxcart raw]$ sudo gatttool -b 1C:88:79:E0:04:26 -I
[1C:88:79:E0:04:26][LE]> connect
Attempting to connect to 1C:88:79:E0:04:26
Connection successful
Notification handle = 0x0024 value: 01 00 ff ff 
[1C:88:79:E0:04:35][LE]> characteristics 
...
handle: 0x005d, char properties: 0x08, char value handle: 0x005e, uuid: 0000a115-0000-1000-8000-00805f9b34fb
...
handle: 0x0085, char properties: 0x8c, char value handle: 0x0086, uuid: 777445ea-22f0-4254-b206-66aef2ec7540
handle: 0x0088, char properties: 0x8c, char value handle: 0x0089, uuid: 777445ea-22f0-4254-b206-66aef2ec7541
handle: 0x008b, char properties: 0x8c, char value handle: 0x008c, uuid: 777445ea-22f0-4254-b206-66aef2ec7542
handle: 0x008e, char properties: 0x8c, char value handle: 0x008f, uuid: 777445ea-22f0-4254-b206-66aef2ec7543
...
```

```
char-write-cmd 005e 01
char-write-cmd 0086 4884ea83c8282948c2b90e586f2cb301218b472b
char-write-cmd 0089 2939a50b612b6af916ef8e59738391844274
char-write-cmd 008c 488df414bfce005e2f15a375afdd083bcbd9f6c3
char-write-cmd 008f 5bc74d84d19e1a3cab4800087da9439e7520
char-write-cmd 0086 488d6954bfe8f41ae328227a09db45e91bcb0c82
char-write-cmd 0089 5ae376a8d2afab543ede06719a28d1243229
char-write-cmd 008c 488d1d529ce96394c44bdd69ae19eb676cc436ab
char-write-cmd 008f 2092402d81edf9211b855ef7ad0a939be5fc5570
char-write-cmd 0086 488d92cec90563a44dbbe8be98e333d9a836daaa
char-write-cmd 0089 c08440699ea23041f619c962647fff52b06f1940
char-write-cmd 008c 488d92cee3abc2a5e21f50cfd471be34ab3bbcad
char-write-cmd 008f 1942d6d10bafc74249b9ac4f0890fea8
char-write-cmd 0086 488e4dade960dea889819c35aff73171ded06228
char-write-cmd 0089 74391806e1e6e3d56796cde588a55b5694
char-write-cmd 008c 488ffc168e17525d0efd21694f8b6605c7952ffc
char-write-cmd 008f 7c1240102ee7d4631c16356fda733c23f34880
char-write-cmd 0086 489165359402097e59c7e7585260067565e8f20c
char-write-cmd 0089 ac8fe000be57b648eb39c5cd5f5b5d0ae42d06
char-write-cmd 008c 48916b2e990fb3400092d0bfb29b4f388482fa24
char-write-cmd 008f 71ebb1785a93483c81bb85395e8420
char-write-cmd 0086 48bec2ee8844d4eb9b04e6a659b5a4cffa2acea7
char-write-cmd 0089 7d2648b81ec35743a7bf856571b67874ef9d
char-write-cmd 008c 48bebf0772147570e9eade4e1a5f6bcec08662e3
char-write-cmd 008f 5541d65d63793ccc8c13b3fb75742b30a0
char-write-cmd 0086 48be9d85f7d8d919c1f7fe2119006b51ed1dbe34
char-write-cmd 0089 266c602b444361157c02aaa5ef1c9eaaaa6d
char-write-cmd 008c 48bea92786587f25ed5465e77bbc6604ce4a405a
char-write-cmd 008f 44801908b79c963f34eb871bd3164ce9228ed2
char-write-cmd 0086 48be8703b611904735c7d8acd1910a62857c7ddb
char-write-cmd 0089 7ec5be7a312f5f7d740ecc522397909b59f410
char-write-cmd 008c 48be770d7fceb325b2409c8f76f6ce6b3313f74f
char-write-cmd 008f cdb301716ebab59f65600a3aaef55642d7911dc4
char-write-cmd 0086 48a8344887e0da169a94309a4a8cbadeca4f5bc7
char-write-cmd 0089 2760964c44a99e6be6950fd2062b7e2e6d1927
char-write-cmd 008c 48bd2267915a3c9aca6d0a9451644c838e59dcd3
char-write-cmd 008f 6f345fb6a3a13f722350f17c282dc119bd
char-write-cmd 0086 48bd5948e18365d15566c2237546bb65c1c4051a
char-write-cmd 0089 1eb1636fb5ce80717b81e823bff9d720
char-write-cmd 008c 48bd497494d4709e398ba9a2448d88fea2771638
char-write-cmd 008f 417e688171a9d506e1b62b2dbdb41b8b1a7e8c18
char-write-cmd 0086 48bd11c70dc9a05cd60cc5af1573ccc59f0871c5
char-write-cmd 0089 e8ea3f4f22d9aaa2f1d8410ab6f2f91a78ba
char-write-cmd 008c 48bd3ccb366e9e351d0200e2d83e0695d85338ec
char-write-cmd 008f a2457f7404842fb9709ba317d7a50d529682fde0
char-write-cmd 0086 48bd0df8efd04cf751067a83af5427ae0d907e10
char-write-cmd 0089 7663a39ac3d0e1b84e5406f5ac79d651d7c84e76
char-write-cmd 008c 48bc150fc0742dea576422a4cdeb724dff69bbf0
char-write-cmd 008f 1d64d198479915b132a538f7a2f58152a3821780
char-write-cmd 0086 48b9869bc088822d8c46274977033bc6a45f52bf
char-write-cmd 0089 11245662534cd1d8a95ce5d0c2dbadb882b8e3
char-write-cmd 008c 48944dc0f49d36468a6af880d5984838083f99a0
char-write-cmd 008f b6b74d48f9e10fdbed50a4c9d6238d65d1216ccf
char-write-cmd 0086 4894a802bf481744bacad83ad3fdb2f603966928
char-write-cmd 0089 425f3376ab7d4cb43f5c1e6988d20b9bd046ce48
char-write-cmd 008c 48bd3dd9d3cf2981a3de51568c33f2738e3e2e6b
char-write-cmd 008f e897dfc5cf469c295d3711b922831e07f8
char-write-cmd 0086 48bd4f423512e4d0a12870fdb9cb947f030c6c20
char-write-cmd 0089 bbe285d8b11fd76f6ae9c9384d61e25bd2ce1f9c
char-write-cmd 008c 48bd4423503ab0289a02c404271d2f1ee6d767c3
char-write-cmd 008f 3e636254a88d344c5e969198a797adfd840a5f
char-write-cmd 0086 48bd60da939b4af8849959a3ecdf5c7fecec8e2c
char-write-cmd 0089 52ecf37dbc90ca9e6b4a668fafb82fc68b828eb6
char-write-cmd 008c 48bd6eeada79c18e64a87364b9431f50cc767f8f
char-write-cmd 008f 8816e5261ec83216111754f304eef4e6f7b0
char-write-cmd 0086 48bd7210c99817a7cbedc14bae8983d0e667d7d8
char-write-cmd 0089 45d2185fbe7bd295b64390408747404ed190
char-write-cmd 008c 48bd6eabd3a45bb7cfc706c8bf73eb9f3406cc57
char-write-cmd 008f 7552a71dcc34ccb6062a29af95cf8a871051c080
char-write-cmd 0086 48bd54e3a19c1faba8a0bd9d3a41e80cff51b0a5
char-write-cmd 0089 1ed4e4e840156ec817263a6e645bea2b4d
char-write-cmd 008c 48bd19f3c1dd8abec476626b5f699ebe5542164a
char-write-cmd 008f a44988cacfdbb0cf75cbfbfe8fabdd26fb1e
char-write-cmd 0086 48bcbf56aac949f9db222ef2bdc4878ad762653b
char-write-cmd 0089 f21742715113ccaedb9a452b46906a7d5b9070
char-write-cmd 008c 48bc9a9cbb5b8c7447c63f9279fb4b63874fbb73
char-write-cmd 008f f5a32b7adcab3384bb0c007d6f8c7bd9fa55fb8c
char-write-cmd 0086 48bc6907a6c441fd5560559aeac16c43dd866b1e
char-write-cmd 0089 327c662054c609053cce972860
char-write-cmd 008c 48bc6a15f0489a9f5e4891148956e289b96f900c
char-write-cmd 008f 1fe6376179c2cf933aaa76731ac7a0
char-write-cmd 0086 48bbfba007306d994b98b184407993925274ef3f
char-write-cmd 0089 602926e19e5d61acd028b976628cd17a1ac0
char-write-cmd 008c 48bc422d89ebb555e251643f2ff428682912a349
char-write-cmd 008f 30b12ee772feacaab5415c3c439283811ed45a40
char-write-cmd 0086 48bc2834622d4938f318b3c05f241d7aadee33d0
char-write-cmd 0089 b7a7adbe7c42f8ada515829b866ff10e3ea340
char-write-cmd 008c 488593fa8a02c4ef8aeaa767f1306f9b1c35a5ea
char-write-cmd 008f 047cb89743ce4cae01600ed9e9abf6ab
char-write-cmd 0086 48859e3c6f083f9e698f8fab542812b6debc1003
char-write-cmd 0089 be131d021416eb1f891e21989b84a4c9ae86c0
char-write-cmd 008c 4885bd9cf8708d118ebcdca0ebf4fe49688cab84
char-write-cmd 008f 8a1ae442742bd7e7f281b9aa00dfd6a2
char-write-cmd 0086 488592ea807fda4b50b503f5e66d623ffb703e07
char-write-cmd 0089 15a25dabb3f6a4781504ae2c430a7e1fa0
char-write-cmd 005e 00
```