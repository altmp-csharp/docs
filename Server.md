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
main: "AltV.Net.Example.dll",
client-main: "client.mjs",
client-files: [ "client.mjs" ]
```

server structure
modules -> 
            csharp-module.dll
resources ->
            my-example-resource ->
                                    AltV.Net.Example.dll
                                    reosurce.cfg
                                    {any_dll_dependency} AltV.Net.dll, mysql.dll...
altv-server.exe

## Events

## Vehicle

## Player

