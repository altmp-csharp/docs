# Server API

```csharp
namespace AltV.Net.Example
{
    public class SampleResource : IResource
    {
        public void OnStart()
        {
            Alt.On<string>("test", s => { Alt.Log("test=" + s); });
            
            Alt.On("test", args => { Alt.Log("args=" + args[0]); });
            
            Alt.Emit("test", "bla");
            
            Alt.On<string>("test2", test2);
            
            Alt.On<string, bool>("test3", test3);
            
            Alt.On("test4", simpleTest);
            
            Alt.On<object, object[], string, string[], IVehicle>("test5", supportedTypes);
            
            Alt.OnPlayerConnect += OnPlayerConnect;
            Alt.OnPlayerDisconnect += OnPlayerDisconnect;
            Alt.OnEntityRemove += OnEntityRemove;
        }

        public void OnStop()
        {
        }
        
        private void OnPlayerConnect(IPlayer player, string reason)
        {
        }

        private void OnPlayerDisconnect(IPlayer player, string reason)
        {
        }

        private void OnEntityRemove(IEntity entity)
        {
        }
        
        public void test2(string test) {
            
        }
        
        public bool test3(string test) {
            
        }
        
        public void simpleTest(object[] args) {
        
        }
        
        // Supported types bool, int, uint, long, ulong, double, string, IVehicle, IPlayer, IBlip, {supported_type}[], Dictionary<string, {supported_type}>
        // Dictionary supports only strings for keys
        // When defining object it will accept any supported type including dictionary and arrays
        // Arrays and dictionaries are supporting any type that is supported, an array could create another array that could create another array ect.
        public void supportedTypes(object obj, object[] objArr, string str, string[] strArray, IVehicle vehicle, IPlayer player) {
            var dict = new Dictionary<string, IVehicle>()
            {
                ["test"] = vehicle,
                ["test2"] = vehicle,
                ["test3"] = vehicle
            };
            player.Call("test_client_event", "test", vehicle, dict);
        }
    }
}
```

resource.cfg :
```
type: "csharp",
main: "AltV.Net.Example.dll"
```
```
server structure
modules -> 
            csharp-module.dll
resources ->
            my-example-resource ->
                                    AltV.Net.Example.dll
                                    reosource.cfg
                                    {any_dll_dependency} AltV.Net.dll, mysql.dll...
altv-server.exe
```

for client resource.cfg :
```
type: "js",
client-main: "client.mjs",
client-files: [ "client.mjs" ]
```
```
server structure
resources ->
            my-example-client-resource ->
                                    client.mjs
                                    resource.cfg
altv-server.exe
```

for dlc resource.cfg
```
{"main":"__stream.cfg","type":"dlc"}
```

```__stream.cfg```
```
{
  "files": [
    "stream/assets/vehiclemods/sk_atmp_c.yft",
    "stream/assets/vehiclemods/sk_atmp_m.yft",
    "stream/assets/vehiclemods/sk_exh1.yft",
    "stream/assets/vehiclemods/sk_exh2.yft",
    "stream/assets/vehiclemods/sk_exh3.yft",
    "stream/assets/vehiclemods/sk_kaput_b.yft",
    "stream/assets/vehiclemods/sk_kaput_k.yft",
    "stream/assets/vehiclemods/sk_otmp_lip.yft",
    "stream/assets/vehiclemods/sk_otmp_m.yft",
    "stream/assets/vehiclemods/sk_otmp_split.yft",
    "stream/assets/vehiclemods/sk_skirt_c.yft",
    "stream/assets/vehiclemods/sk_skirt_s.yft",
    "stream/assets/vehiclemods/sk_sp_cc.yft",
    "stream/assets/vehiclemods/sk_sp_cr.yft",
    "stream/assets/vehiclemods/sk_sp_lip.yft",
    "stream/assets/vehiclemods/sk_top_mugen.yft",
    "stream/assets/vehicles/ap2.yft",
    "stream/assets/vehicles/ap2.ytd",
    "stream/assets/vehicles/ap2_hi.yft",
    "stream/assets/vehicles/vehicles_s2000_interior.ytd"
  ],
  "meta": {
    "stream/carcols.meta": "CARCOLS_FILE",
    "stream/carvariations.meta": "VEHICLE_VARIATION_FILE",
    "stream/handling.meta": "HANDLING_FILE",
    "stream/vehicles.meta": "VEHICLE_METADATA_FILE"
  }
}
```

server structure
```
resources -> 
            stream-ap2 ->
                            resource.cfg
                            __stream.cfg
                            stream ->
                                       assets -> 
                                                ...
                                       xyz.meta
                                       ...
            
altv-server.exe


## Events

## Vehicle

## Player

