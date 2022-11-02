Mosquitto
=========

Integrated Cinematics notes
----------------------------

MqttUtilities uses a very old version of libmosquitto - v1.4.8. This branch is
based on v1.4.8 with a small modification to build with visual studio 2022.

Ideally, we should investigate whether we can update the version to something
newer, but for now we're using v1.4.8 like MqttUtilities.

We need to build this because MqttUtilities comes with a debug build of
mosquitto.dll which depends on vcruntime140d.dll which isn't a redistributable
component (although it does get installed as part of visual studio).

To build this on a windows machine, you need

- Visual Studio 2022 or later
- modern (post 3.0) cmake, available at the path 

Open a "Developer Command Prompt for VS 2022" command window (this is in the
start menu when you install visual studio), and navigate to the base of this
Mosquitto directory. Then,

```
mkdir _build
cd _build
cmake -DWITH_TLS=False -DWITH_THREADING=False ..
start mosquitto.sln
```

Then, in visual studio, build the `RelWithDebInfo` configuration. This will produce the files

```
mosquitto/_build/lib/RelWithDebInfo/mosquitto.dll
mosquitto/_build/lib/RelWithDebInfo/mosquitto.exp
mosquitto/_build/lib/RelWithDebInfo/mosquitto.lib
mosquitto/_build/lib/RelWithDebInfo/mosquitto.pdb
mosquitto/_build/lib/cpp/RelWithDebInfo/mosquittopp.dll
mosquitto/_build/lib/cpp/RelWithDebInfo/mosquittopp.exp
mosquitto/_build/lib/cpp/RelWithDebInfo/mosquittopp.lib
mosquitto/_build/lib/cpp/RelWithDebInfo/mosquittopp.pdb
```

Copy these files into our general repository.

General (non-Integrated-Cinematics) notes
-------------------------------

Mosquitto is an open source implementation of a server for version 3.1 and
3.1.1 of the MQTT protocol.

See the following links for more information on MQTT:

- Community page: <http://mqtt.org/>
- MQTT v3.1.1 standard: <http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.html>

Mosquitto project information is available at the following locations:

- Main homepage: <http://mosquitto.org/>
- Find existing bugs: <https://bugs.eclipse.org/bugs/buglist.cgi?product=Mosquitto>
- Submit a bug: <https://bugs.eclipse.org/bugs/enter_bug.cgi?product=Mosquitto>
- Source code repository: <http://git.eclipse.org/c/mosquitto/org.eclipse.mosquitto.git/>

There is also a public test server available at <http://test.mosquitto.org/>

Mosquitto was written by Roger Light <roger@atchoo.org>
