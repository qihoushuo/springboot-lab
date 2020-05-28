 import com.fasterxml.jackson.databind.ObjectMapper; 
 import com.hazelcast.config.Config; 
 import com.hazelcast.core.Hazelcast; 
 import com.hazelcast.core.HazelcastInstance;
 
 =====================================================
 
 import org.springframework.web.socket.WebSocketSession;
 import java.util.concurrent.CopyOnWriteArrayList;
 
 List<WebSocketSession> sessions = new CopyOnWriteArrayList<>();

===========================================================================

I would like to get the value of a key, however the Map is large so I don't want it to be completely loaded into memory. So if I do something like:
## hazelcast.getReplicatedMap(name).get(key)
will it load the whole map into memory then get the value?
If yes, is there a way to get the value of a key without loading everything into memory?

Ans:
With the replicated map the whole map is replicated to all members in the cluster. So it will always be fully in memory on those members.
On the client side, only the value is pulled into memory when you call replicatedMap.get(key)


==============================================================

spring-cache is just an abstraction over a cache implementation. If you make sure to have hazelcast-spring on the classpath, Hazelcast will be chosen as the implementation, and you can configure it however you want. If you want control over the initialization sequence e.g. bean X before bean Y, you should pass X as an argument to the method that return Y. In the code above, Spring guarantees the CacheManager is instantiated before calling the run() method. 
