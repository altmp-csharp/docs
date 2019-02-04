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
            
            Alt.On("test5", supportedTypes);
        }

        public void OnStop()
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
        public void supportedTypes(object obj, object[] objArr, string str, string[] strArray, IVehicle vehicle) {
        
        }
    }
}
```

## Events

## Vehicle

## Player

