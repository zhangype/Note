# ����֪ʶ
## Spring Cloud���
&nbsp;&nbsp;Spring Cloud ��һ������ Spring Boot ʵ�ֵ�΢����ܹ��������ߡ���Ϊ΢����ܹ����漰���ù�������������·��������·�ɡ�΢����ȫ���������߾�ѡ���ֲ�ʽ�Ự�ͼ�Ⱥ״̬����Ȳ����ṩ��һ�ּ򵥵Ŀ�����ʽ��  
&nbsp;&nbsp;΢����ǿ��������֮����С������񡱵ĵ��ã�����������һ���ԣ�ֻҪ�����������Ĵ���״̬��һ�µļ��ɡ����ڹ����з��ִ���ͨ���������������д���ʹ�ô��������ܹ��ﵽ���յ�һ���ԡ�  
&nbsp;&nbsp;Spring Cloud �����˶������Ŀ��  
&nbsp;&nbsp;��**Spring Cloud Config**�����ù����ߣ�֧��ʹ�� Git �洢�������ݣ�����ʹ����ʵ��Ӧ�����õ��ⲿ���洢����֧�ֿͻ���������Ϣˢ�¡�����/�����������ݵȡ�  
&nbsp;&nbsp;��**Spring Cloud Netflix**������������Զ��Netflix OSS ��Դ�׼��������ϡ�  
&nbsp;&nbsp;&nbsp;&nbsp;��**Eureka**�����������������������ע�����ġ�����ע���뷢�ֻ��Ƶ�ʵ�֡�  
&nbsp;&nbsp;&nbsp;&nbsp;��**Hystrix**���ݴ���������ʵ�ֶ�·��ģʽ���������������г��ֵ��ӳٺ͹����ṩǿ����ݴ�������  
&nbsp;&nbsp;&nbsp;&nbsp;��**Ribbon**���ͻ��˸��ؾ���ķ�����������  
&nbsp;&nbsp;&nbsp;&nbsp;��**Feign**������ Ribbon �� Hystrix ������ʽ������������  
&nbsp;&nbsp;&nbsp;&nbsp;��**Zuul**������������ṩ����·�ɡ����ʹ��˵ȹ��ܡ�  
&nbsp;&nbsp;&nbsp;&nbsp;��**Archaius**���ⲿ�����������  
&nbsp;&nbsp;��**Spring Cloud Bus**���¼�����Ϣ�������ڴ�����Ⱥ�е�״̬�仯���¼����Գ��������Ĵ�������������̬ˢ�����õȡ�  
&nbsp;&nbsp;��**Spring Cloud Cluster**����� Zookeeper��Redis��Hazelcast��Consul ��ѡ���㷨��ͨ��״̬ģʽ��ʵ�֡�  
&nbsp;&nbsp;��**Spring Cloud Cloudfoundry**���� Pivotal Cloudfoundry ������֧�֡�  
&nbsp;&nbsp;��**Spring Cloud Consul**�������������ù����ߡ�  
&nbsp;&nbsp;��**Spring Cloud Stream**��ͨ�� Redis��Rabbit ���� Kafka ʵ�ֵ�����΢���񣬿���ͨ���򵥵�����ʽģ�������ͺͽ�����Ϣ��  
&nbsp;&nbsp;��**Spring Cloud AWS**�����ڼ����� Amazon Web Service �������  
&nbsp;&nbsp;��**Spring Cloud Security**����ȫ���߰����ṩ Zuul �����ж� OAuth2 �ͻ��������м�����  
&nbsp;&nbsp;��**Spring Cloud Sleuth**��Spring Cloud Ӧ�õķֲ�ʽ����ʵ�֣������������� Zipkin��  
&nbsp;&nbsp;��**Spring Cloud ZooKeeper**������ ZooKeeper �ķ����������ù��������  
&nbsp;&nbsp;��**Spring Cloud Starters**��Spring Cloud �Ļ�����������ǻ���Spring Boot �����Ŀ�Ļ�������ģ�顣  
&nbsp;&nbsp;��**Spring Cloud CLI**�������� Groovy �п��ٴ��� Spring Cloud Ӧ�õ� Spring Boot CLI �����  
&nbsp;&nbsp;��... ...  
# ΢���񹹽���Spring Boot
## ����˳��
&nbsp;&nbsp;1�����������д���Ĳ�����  
&nbsp;&nbsp;2��SPRING_APPLICATION_JSON �е����ԡ�SPRING_APPLICATION_JSON ����JSON ��ʽ������ϵͳ���������еĵ����ݡ�  
&nbsp;&nbsp;3��java:comp/env �е� JNDI ���ԡ�  
&nbsp;&nbsp;4��Java ��ϵͳ���ԣ�����ͨ��System.getProperties()��ȡ�����ݡ�  
&nbsp;&nbsp;5������ϵͳ�Ļ���������  
&nbsp;&nbsp;6��ͨ��random.*���õ�������ԡ�  
&nbsp;&nbsp;7��λ�ڵ�ǰӦ�� jar ��֮�⣬��Բ�ͬ{profile}�����������ļ����ݣ�����application-{profile}.properties ���� YAML ����������ļ���  
&nbsp;&nbsp;8��λ�ڵ�ǰӦ�� jar ��֮�ڣ���Բ�ͬ{profile}�����������ļ����ݣ�����application-{profile}.properties ���� YAML ����������ļ���  
&nbsp;&nbsp;9��λ�ڵ�ǰӦ��jar��֮��� application.properties �� YAML �������ݡ�  
&nbsp;&nbsp;10��λ�ڵ�ǰӦ��jar��֮�ڵ� application.properties �� YAML �������ݡ�  
&nbsp;&nbsp;11����@Configurationע���޸ĵ����У�ͨ�� @PropertySource ע�ⶨ������ԡ�  
&nbsp;&nbsp;12��Ӧ��Ĭ�����ԣ�ʹ�� SpringApplication.setDefaultProperties ��������ݡ�  
&nbsp;&nbsp;���ȼ��������˳���ɸߵ��ͣ�����ԽС���ȼ�Խ�ߡ�  
## ��������
&nbsp;&nbsp;spring-boot-starter-actuator ģ���ʵ�ֶ���ʵʩ΢�������С�Ŷ���˵��������Ч��ʡȥ������ټ��ϵͳ�ڲɼ�ָ��ʱ�Ŀ�������  
### ԭ���˵�
&nbsp;&nbsp;**Ӧ��������**����ȡӦ�ó����м��ص�Ӧ�����á������������Զ������ñ������Spring Boot Ӧ��������ص���������Ϣ��  
&nbsp;&nbsp;**����ָ����**����ȡӦ�ó������й��������ڼ�صĶ���ָ�꣬�����ڴ���Ϣ���̳߳���Ϣ��HTTP ����ͳ�Ƶȡ�  
&nbsp;&nbsp;**����������**���ṩ�˶�Ӧ�õĹرյȲ����๦�ܡ�  
#### Ӧ��������
&nbsp;&nbsp;��/**autoconfig**���ö˵�������ȡӦ�õ��Զ������ñ��棬���а��������Զ������õĺ�ѡ�ͬʱ���г���ÿ����ѡ���Ƿ������Զ������õĸ����Ⱦ��������ö˵���Է�����ҵ�һЩ�Զ�������Ϊʲôû����Ч�ľ���ԭ�򡣸ñ������ݽ��Զ����������ݷ�Ϊ�����������֣�  
&nbsp;&nbsp;&nbsp;&nbsp;��/positiveMatches �з��ص�������ƥ��ɹ����Զ������á�  
&nbsp;&nbsp;&nbsp;&nbsp;��/negativeMatches �з��ص�������ƥ�䲻�ɹ����Զ������á�  
&nbsp;&nbsp;��/**beans**���ö˵�������ȡӦ���������д���������Bean��  
&nbsp;&nbsp;��/**configprops**���ö˵�������ȡӦ�������õ�������Ϣ���档  
&nbsp;&nbsp;��/**env**���ö˵���/configprops ��ͬ����������ȡӦ�����п��õĻ������Ա��档��������������JVM ���ԡ�Ӧ�õ��������ԡ��������еĲ�����  
&nbsp;&nbsp;��/**mappings**���ö˵������������� Spring MVC �Ŀ�����ӳ���ϵ���档  
&nbsp;&nbsp;��/**info**���ö˵���������һЩӦ���Զ������Ϣ��Ĭ������£��ö˵�ֻ�᷵��һ���յ� JSON ���ݡ������� application.properties �����ļ���ͨ�� info ǰ׺������һЩ���ԣ��磺  
> info.app.name=myboot
> info.app version=v1.0.0
#### ����ָ����
&nbsp;&nbsp;����ָ����˵��ṩ�ı��������Ƕ�̬�仯�ģ���Щ���ṩ��Ӧ�ó��������й����е�һЩ������Ϣ������˵�ڴ�ʹ�������HTTP����ͳ�ơ��ⲿ��Դָ��ȡ�  
&nbsp;&nbsp;��/**metrics**���ö˵��������ص�ǰӦ�õĸ�����Ҫ����ָ�꣬�����ڴ���Ϣ���߳���Ϣ������������Ϣ�ȡ�  
&nbsp;&nbsp;��/**health**���ö˵��ȡӦ�õĸ��ཡ��ָ����Ϣ��  
&nbsp;&nbsp;��/**dump**���ö˵�������¶���������е��߳���Ϣ��  
&nbsp;&nbsp;��/**trace**���ö˵��������ػ����� HTTP ������Ϣ��  
#### ����������
&nbsp;&nbsp;����������˵�ӵ�и�ǿ��Ŀ����������Ҫʹ�õĻ�����Ҫͨ���������ÿ�����  
> endpoints.shutdown.enabled=true

&nbsp;&nbsp;��/**shutdown**���ö˵����ʵ�ֹر�Ӧ�õ�Զ�̲�����  
# ��������Spring Cloud Eureka
## ��������
&nbsp;&nbsp;��**����ע��**���ڷ����������У�ͨ�����ṹ��һ��ע�����ģ�ÿ������Ԫ��ע�����ĵǼ��Լ��ṩ�ķ��񣬽�������˿ںš��汾�š�ͨ��Э���һЩ������Ϣ��֪ע�����ģ�ע�����İ�������������֯�����嵥��  
&nbsp;&nbsp;��**������**���ڷ����������У������ĵ��ò���ͨ��ָ�������ʵ����ַʵ�֣�����ͨ��������������������ʵ�֡�  
&nbsp;&nbsp;��Ĭ�������£�����ע�����ĻὫ�Լ���Ϊ�ͻ��˳���ע���Լ�����Ҫ�������Ŀͻ���ע����Ϊ��������������ã�  
> eureka.client.register-with-eureka=false
> eureka.client.fetch-registry=false

&nbsp;&nbsp;��**eureka.client.register-with-eureka**��������ע������ע���Լ���  
&nbsp;&nbsp;��**eureka.client.register-with-eureka**��������Ҫ��������  
## �߿���ע������
&nbsp;&nbsp;Eureka Server �ĸ߿���ʵ���Ͼ��ǽ��Լ���Ϊ��������������ע������ע���Լ��������Ϳ����γ�һ�黥��ע��ķ���ע�����ģ���ʵ�ַ����嵥���໥ͬ�����ﵽ�߿��õ�Ч����  
## ������������
&nbsp;&nbsp;�����ֵ������� Eureka �Ŀͻ�����ɣ����������ѵ������� Ribbon ��ɡ�Ribbon ��һ������ HTTP �� TCP �Ŀͻ��˸��ؾ���������������ͨ���ͻ��������õ� ribbonServerList ������б�ȥ��ѯ�����Դﵽ���ؾ�������á�  �� Ribbon �� Eureka ����ʹ��ʱ��Ribbon �ķ���ʵ���嵥 RibbonServerList �ᱻ DiscoveryEnabledNIWSServerList ��д����չ�ɴ� Eureka ע�������л�ȡ������б�ͬʱ��Ҳ���� NIWSDiscoveryPing ��ȡ�� IPing������ְ��ί�и� Eureka ��ȷ��������Ƿ��Ѿ�������  

## Eureka���
### �����������
#### �����ṩ��
##### ����ע��
&nbsp;&nbsp;�������ṩ�ߡ���������ʱ���ͨ������REST����ķ�ʽ���Լ�ע�ᵽ Eureka Server �ϣ�ͬʱ��������������һЩԪ������Ϣ�� Eureka Server ���յ���� REST ����֮�󣬽�Ԫ������Ϣ�洢��һ��˫��ṹ Map �У����е�һ��� key �Ƿ��������ڶ���� key �Ǿ�������ʵ������  
&nbsp;&nbsp;���ڷ���ʵ����ѡ��Eureka ���� Region �� Zone �ĸ��һ�� Region �п��԰������ Zone ��ÿ������ͻ�����Ҫ��ע�ᵽһ�� Zone �У�����ÿ���ͻ��˶�Ӧһ�� Region �� һ�� Zone ���ڽ��з�����õ�ʱ�����ȷ���ͬ��һ�� Zone �еķ����ṩ���������ʲ������ͷ��������� Zone ��  
##### ������Լ
&nbsp;&nbsp;��ע��������ע��֮�󣬷����ṩ�߻�ά��һ������������������ Eureka Server���������ʹ�á�  
#### ����������
&nbsp;&nbsp;���������������ߵ�ʱ�����ᷢ��һ�� REST ���������ע�����ģ�����ȡע��ķ����嵥��Ϊ�����ܿ��ǣ� Eureka Server ��ά��һ��ֻ���ķ����嵥�����ظ��ͻ��ˣ�ͬʱ�û����嵥ÿ��30�����һ�Ρ�  
##### �������
&nbsp;&nbsp;���ڷ���ʵ����ѡ��Eureka���� Region �� Zone �ĸ��һ�� Region �п��԰������ Zone��ÿ���ͻ�����Ҫ��ע�ᵽһ�� Zone �У�����ÿ���ͻ��˶�Ӧһ�� Region ��һ�� Zone���ڽ��з�����õ�ʱ�����ȷ���ͬ��һ�� Zone �еķ����ṩ���������ʲ������ͷ��������� Zone��  
##### ��������
&nbsp;&nbsp;������ʵ�����������Ĺرղ���ʱ�����ᴥ��һ���������ߵ� Rest ����� Eureka Server����֪����ע�����ġ�������ڽ��յ�����֮�󣬽��÷���״̬��Ϊ���ߣ�DOWN�������ɸ������¼�������ȥ��  
#### ����ע������
##### ʧЧ�޳�
&nbsp;&nbsp;Eureka Server ��������ʱ��ᴴ��һ����ʱ����Ĭ��ÿ��һ��ʱ�䣨Ĭ��Ϊ60�룩����ǰ�嵥�г�ʱ��Ĭ��Ϊ90�룩û����Լ�ķ����޳���ȥ��  
##### ���ұ���
&nbsp;&nbsp;Eureka Server �������ڼ䣬��ͳ������ʧ�ܵı�����15����֮���Ƿ����85%��������ֵ��ڵ������ Eureka Server �Ὣ��ǰ��ʵ��ע����Ϣ��������������Щʵ��������ڣ������ܱ�����Щע����Ϣ�����ǣ�����α�������ʵ�����������⣬��ô�ͻ��˺������õ�ʵ���Ѿ������ڵķ���ʵ��������ֵ���ʧ�ܵ���������Կͻ��˱���Ҫ���ݴ���ƣ��������ʹ���������ԣ���·���Ȼ��ơ�  
### ����ע��������
&nbsp;&nbsp;���ڷ���ע�����������Ϣ������ͨ���鿴 org.springframework.cloud.netflix.eureka.EurekaClientConfigBean ��Դ������ȡ��ϸ���ݣ���Щ������Ϣ���� eureka.client Ϊǰ׺��  
### ����ʵ��������
&nbsp;&nbsp;���ڷ���ʵ�����������Ϣ������ͨ���鿴 org.springframework.cloud.netflix.eureka.EurekaInstanceConfigBean ��Դ������ȡ��ϸ���ݣ���Щ������Ϣ���� eureka.instance Ϊǰ׺��  
#### Ԫ����
&nbsp;&nbsp;��  org.springframework.cloud.netflix.eureka.EurekaInstanceConfigBean ��������Ϣ�У���һ�󲿷����ݶ��ǶԷ���ʵ��Ԫ���ݵ����á�Ԫ������ Eureka �ͻ����������ע�����ķ���ע������ʱ�������������������Ϣ�Ķ������а�����һЩ��׼����Ԫ���ݣ�����������ơ�ʵ�����ơ�ʵ��IP��ʵ���˿ڵ����ڷ����������Ҫ��Ϣ���Լ�һЩ���ڸ��ؾ�����Ի���������������;���Զ���Ԫ���ݡ�  
# �ͻ��˸��ؾ��⣺Spring Cloud Ribbon
&nbsp;&nbsp; Spring Cloud Ribbon ��һ������ HTTP �� TCP �Ŀͻ��˸��ؾ��⹤�ߣ������� Netflix Ribbon ʵ�֡�  
### �Զ�������
&nbsp;&nbsp; ͨ���Զ������õ�ʵ�֣��������ɵ�ʵ�ֿͻ��˸��ؾ��⡣ͬʱ�����һЩ���Ի�����Ҳ���Է�����滻Ĭ��ʵ�֡�ֻ��Ҫ�� Spring Boot Ӧ���д�����Ӧ��ʵ��ʵ�����ܸ�����ЩĬ�ϵ�����ʵ�֡�����������������ݣ����ڴ����� PingUrl ʵ��������Ĭ�ϵ� NoOpPing �Ͳ��ᱻ������  
``` java
@Configuration
public class MyRibbonConfiguration {
	@Bean
	public IPing ribbonPing (IClientConfig config) {
		return new PingUrl();
	}
}
```
&nbsp;&nbsp; ���⣬Ҳ����ͨ��ʹ�� @RibbonClient ע����ʵ�ָ�ϸ���ȵĿͻ������ã���������Ĵ���ʵ����Ϊ hello-service ����ʹ�� HelloServiceConfiguration �е����á�  
``` java
@Configuration
@RibbonClient(name = "hello-service", configuration = HelloServiceConfiguration.class)
public class RibbonConfiguration {
}
```
### Camden �汾�� RibbonClient ���õ��Ż�
&nbsp;&nbsp; ����ֱ��ͨ��&lt;clientName&gt;.ribbon.&lt;key&gt;=&lt;value&gt;����ʽ�������á����罫 hello-service ����ͻ��˵� IPing �ӿ�ʵ���滻Ϊ PingUrl��ֻ���� application.properties �����������������ݼ��ɣ�  
> hello-service.ribbon.NFLoadBalancePingClassName=com.netflix.loadbalancer.PingUrl

&nbsp;&nbsp; ���� hello-service Ϊ�������� NFLoadBalancePingClassName ��������ָ������� IPing �ӿ�ʵ���ࡣ  
&nbsp;&nbsp; ȫ�����÷�ʽ��ʹ�� ribbon.&lt;key&gt;=&lt;value&gt;��ʽ�������ü��ɡ����У�&lt;key&gt;������  Ribbon �ͻ������õĲ�������&lt;value&gt;������˶�Ӧ������ֵ��  
> ribbon.ConnectTimeout=250

### �� Eureka ���
&nbsp;&nbsp; �� Spring Cloud ��Ӧ����ͬʱ���� Spring Cloud Ribbon �� Spring Cloud Eureka ����ʱ���ᴥ�� Eureka ��ʵ�ֵĶ� Ribbon �Զ������á�  
### ���Ի���
&nbsp;&nbsp; Spring Cloud Euraka ʵ�ֵķ����������ǿ���� CAP ԭ���е� AP������������ɿ��ԣ����� ZooKeeper ����ǿ�� CP ��һ���ԡ��ɿ��ԣ��ķ��������ܵ����������ǣ� Eureka Ϊ��ʵ�ָ��ߵķ�������ԣ�������һ����һ���ԣ��ڼ������������Ը���ܹ���ʵ��Ҳ������������ʵ������  
# �����ݴ����� Spring Cloud Hystrix
## ��������
![Hytrix����ͼ](./Hytrix����ͼ.png)
&nbsp;&nbsp;**1������ HystrixCommand �� HystrixObservableCommand ����**  
&nbsp;&nbsp;**2������ִ��**  
&nbsp;&nbsp;HystrixCommand ʵ������������ִ�з�ʽ��  
&nbsp;&nbsp;��execute()��ͬ��ִ�У��������ķ��񷵻�һ����һ�Ľ�����󣬻����ڷ��������ʱ���׳��쳣��  
&nbsp;&nbsp;��queue()���첽ִ�У�ֱ�ӷ���һ�� Future �������а����˷���ִ�н���ʱҪ���صĵ�һ�������  
``` java
R value = command.execute();
Future<R> fValue = command.queue();
```
&nbsp;&nbsp;HystrixObservableCommand ʵ������������ִ�з�ʽ��  
&nbsp;&nbsp;��observe()������ Observable �����������˲����Ķ�����������һ�� HotObservable ��  
&nbsp;&nbsp;��toObservable()��ͬ���᷵�� Observable ����Ҳ�����˲����Ķ��������������ص���һ��Cold Observable��  
``` java
Observable<R> ohValue = command.observe();
Observable<R> ocValue = command.observe();
```
&nbsp;&nbsp;���� Hot Observable �����ۡ��¼�Դ���Ƿ��С������ߡ��������ڴ�������¼����з��������Զ��� Hot Observable ��ÿһ���������ߡ����п��ܴӡ��¼�Դ������;��ʼ�ģ�������ֻ���������������ľֲ����̡�  
&nbsp;&nbsp;Cold Observable ��û�С������ߡ���ʱ�򲢲��ᷢ���¼������ǽ��еȴ���ֱ���С������ߡ�֮��ŷ����¼������Զ���Cold Observable �Ķ����ߣ������Ա�֤��һ��ʼ��������������ȫ�����̡�  
&nbsp;&nbsp;**3������Ƿ񱻻���**  
&nbsp;&nbsp;����ǰ��������󻺴湦���Ƿ����õģ����Ҹ���������У���ô����Ľ���������� Observable �������ʽ���ء�  
&nbsp;&nbsp;**4����·���Ƿ��**  
&nbsp;&nbsp;�����·���Ǵ򿪵ģ���ô Hystrix ����ִ���������ת�ӵ� fallback �����߼�����Ӧ�����8������  
&nbsp;&nbsp;�����·���ǹرյģ���ô Hystrix ������5��������Ƿ��п�����Դ��ִ�����  
&nbsp;&nbsp;**5���̳߳�/�������/�ź����Ƿ�ռ��**  
&nbsp;&nbsp;�����������ص��̳߳غ�������У������ź�������ʹ���̳߳ص�ʱ���Ѿ���ռ������ô Hystrix Ҳ����ִ���������ת�ӵ� fallback �����߼�����Ӧ����ĵ�8������  
&nbsp;&nbsp;**6��HystrixObservableCommand.construct() �� HystrixCommand.run()**  
&nbsp;&nbsp;Hystrix ����ݱ�д�ķ�����������ȡʲô���ķ�ʽȥ������������  
&nbsp;&nbsp;��HystrixCommand.run()������һ����һ�Ľ���������׳��쳣��  
&nbsp;&nbsp;��HystrixObservableCommand.construct() ������һ�� Observable ���������������������ͨ�� onError ���ʹ���֪ͨ��
&nbsp;&nbsp;**7�������·���Ľ�����**  
&nbsp;&nbsp;Hystrix �Ὣ ���ɹ��������ܾ���������ʱ������Ϣ�������·��������·����ά��һ���������ͳ����Щ���ݡ�  
&nbsp;&nbsp;��·����ʹ����Щͳ�������������Ƿ񽫶�·���򿪣�����ĳ�����������������ԡ��۶�/��·����ֱ���ָ��ڽ��������ڻָ��ڽ����󣬸���ͳ�������ж��������δ�ﵽ����ָ�꣬���ٴΡ��۶�/��·����  
&nbsp;&nbsp;**8��fallback����**  
&nbsp;&nbsp;**9�����سɹ�����Ӧ**  
&nbsp;&nbsp;�� Hystrix ����ִ�гɹ�֮�����Ὣ������ֱ�ӷ��ػ����� Observable ����ʽ���ء����巵�ط�ʽȡ���ڵ�2�����������ᵽ�Ķ������4�в�ִͬ�з�ʽ����ͼ���ܽ��������ֵ��÷�ʽ֮���������ϵ��  
![������ϵ](./������ϵ.png)
&nbsp;&nbsp;�� toObservable()��������ԭʼ�� Observable������ͨ���������Ż��������������ִ�����̡�  
&nbsp;&nbsp;�� observe()����toObservable()����ԭʼ Observable ֮���������������������ܹ����Ͽ�ʼ�첽ִ�У�������һ�� Observable ���󣬵���������subscribeʱ�������²��������֪ͨ�������ߡ�  
&nbsp;&nbsp;�� queue()���� toObservable()������ԭʼ Observable ͨ�� toBlocking() ����ת���� BlockingObservable ���󣬲��������� toFuture() f���������첽�� Future ����  
&nbsp;&nbsp;�� execute()���� queue() �����첽��� Future ����֮��ͨ������ get() �����������ȴ�����ķ��ء�  
## ��·��ԭ��
&nbsp;&nbsp;��·�� HystrixCircuitBreaker ���壺  
```java
public interface HystrixCircuitBreaker {

	public static class Factory {...}

	static class HystrixCircuitBreakerImpl implements HystrixCircuitBreaker {...}

	static class NoOpCircuitBreaker implements HystrixCircuitBreaker {...}

	public boolean allowRequest();

	public boolean isOpen();

	void markSuccess();
}
```
&nbsp;&nbsp;��allRequest()��ÿ�� Hystrix ���������ͨ�������ж��Ƿ�ִ�С�  
&nbsp;&nbsp;��isOpen()�����ص�ǰ��·���Ƿ񱻴򿪡�  
&nbsp;&nbsp;��markSuccess()�������պ϶�·����  
&nbsp;&nbsp;��̬�� Factory ��ά����һ�� Hystrix ������ HystrixCircuitBreaker �Ĺ�ϵ���ϣ� ConcurrentHashMap&lt;String, HystrixBreaker&gt; circuitBreakerByCommand������ String ���͵� key ͨ�� HystrixCommandKey ���壬ÿһ�� Hystrix ���Ҫ��һ�� key ����ʶ��ͬһ�� Hystrix ����Ҳ���ڸü������ҵ�����Ӧ�Ķ�·�� HystrixCircuitBreaker ʵ����  
&nbsp;&nbsp;��̬�� NoOpCircuitBreaker ������һ��ʲô�������Ķ�·��ʵ�֣����������е����󣬲��Ҷ�·��״̬ʼ�ձպϡ�  
&nbsp;&nbsp;��̬�� HystrixCircuitBreakerImpl �Ƕ�·���ӿ� HystrixCircuitBreaker ��ʵ���࣬�ڸ����ж������ĸ����Ķ���  
&nbsp;&nbsp;&nbsp;&nbsp;�� HystrixCommandProperties properties����·����Ӧ HystrixCommand ʵ�������Զ���  
&nbsp;&nbsp;&nbsp;&nbsp;�� HystrixCommandMetrics metrics�������� HystrixCommand ��¼�������ָ��Ķ���  
&nbsp;&nbsp;&nbsp;&nbsp;�� AtomicBoolean circuitOpen����·���Ƿ�򿪵ı�־��Ĭ��Ϊfalse��  
&nbsp;&nbsp;&nbsp;&nbsp;�� AtomicLong circuitOpenedOrLastTestedTime����·���򿪻����ϴβ��Ե�ʱ�����  
![��·��ִ���߼�](./��·��ִ���߼�.png)

## ��������
&nbsp;&nbsp;Hystrix ʹ�á��ձ�ģʽ��ʵ���̳߳صĸ��룬����Ϊÿһ���������񴴽�һ���������̳߳أ��Ӷ�ĳ��������������ӳٹ��ߵ������Ҳֻ�ǶԸ���������ĵ��ò���Ӱ�죬������������������������  
&nbsp;&nbsp;����ʹ���̳߳�֮�⣬������ʹ���ź��������Ƶ���������Ĳ����ȣ��ź����Ŀ���Զ���̳߳صĿ���С�����ǲ������ó�ʱ��ʵ���첽���ʡ��� HystrixCommand �� HystrixObservableCommand ��������֧���ź�����ʹ�á�  
&nbsp;&nbsp;��**����ִ��**�������������� execution.isolation.strategy ����Ϊ SEMAPHORE�� Hystrix ��ʹ���ź�������̳߳���������������Ĳ�����  
&nbsp;&nbsp;��**�����߼�**����Hystrix ���Խ����߼��ǣ������ڵ����߳���ʹ���ź�����  

## ʹ�����
&nbsp;&nbsp;Hystrix ����������װ�����������������߼���  
&nbsp;&nbsp;����ͨ���̳еķ�ʽ��ʵ�֣����磺
``` java
public class UserCommand extends HystrixCommand<User> {

    private RestTemplate restTemplate;
    private Long id;

    public UserCommand(Setter setter, RestTemplate restTemplate, Long id) {
        super(setter);
        this.restTemplate = restTemplate;
        this.id = id;
    }

    @Override
    protected UserDTO run() throws Exception {
        return restTemplate.getForObject("http://myboot/sys/user/info/{1}", User.class, id);
    }
}
```
&nbsp;&nbsp;ͨ������ʵ�ֵ� UserCommand���ȿ���ʵ�������ͬ��ִ��Ҳ����ʵ���첽ִ�С�  
&nbsp;&nbsp;**��ͬ��ִ�У�**
``` java
User u = new UserCommand(restTemplate,  1L).execute();
```
&nbsp;&nbsp;**���첽ִ�У�**
``` java
Future<User> futureUser = new UserCommand(restTemplate, 1L).queue();
```
&nbsp;&nbsp;Ҳ����ͨ��@HystrixCommand ע������Ϊ���ŵ�ʵ�� Hystrix ����Ķ��壬�磺  
``` java
public class UserService {
	@Autowired
	private RestTemplate restTemplate;

	@HystrixCommand
	public User getUserById(long id) {
		return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
	}
}
```
&nbsp;&nbsp;���ϵĶ���ķ���ֻ��ͬ����ʵ�ַ�ʽ����Ҫʵ���첽ִ������Ҫ���ⶨ�壬���磺  
``` java
@HystrixCommand
public Fature<User> getUserByIdAsync(final String id) {
	return new AsyncResult<User>() {
		@Override
		public User invoke() {
			return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
		}
	}
}
```
&nbsp;&nbsp;���˴�ͳ��ͬ��ִ�����첽ִ��֮�⣬�����Խ� HystrixCommand ͨ�� Observable ��ʵ����Ӧʽִ�з�ʽ��ͨ������ observe() �� toObservable() �������Է��� Observable ���󣬱��磺  
``` java
Observable<String> ho = new UserCommand(restTemplate, 1L).observe();
Observable<String> co = new UserCommand(restTemplate, 1L).toObservable();
```
&nbsp;&nbsp;��Ȼ HystrixCommand �߱��� observe() �� toObservable() �Ĺ��ܣ���������ʵ����һ���ľ����ԣ������ص�Observable ֻ�ܷ���һ�����ݣ����� Hystrix ���ṩ������һ�����������װ  HystrixObservableCommand ��ͨ����ʵ�ֵ�������Ի�ȡ�ܹ������ε� Observable��  
&nbsp;&nbsp;ʾ���������£�  
``` java
public class UserObservableCommand extends HystrixObservableCommand<User> {
	private RestTemplate restTemplate;
	private Long id;

	public UserObservableCommand(Setter setter, RestTemplate restTemplate, Long id) {
		supper(setter);
		this.restTemplate = restTemplate;
		this.id = id;
	}

	@Override
	protected Observable<User> construct() {
		return Observable.create(new Observable.OnSubscribe<User>() {
			@Override
			public void call (Subscriber<? super User> observer) {
				try {
					if (!observer.isUnsubscribed()) {
						restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
						observer.onNext(user);
						observer.onCompleted();
					}
				} catch (Exception e) {
					observer.onError(e);
				}
			}
		});
	}
}
```
&nbsp;&nbsp;@HystrixCommand ʹ�÷�����  
``` java
@HystrixCommand
public Observable<User> getUserById(final String id) {
	return Observable.create(new Observable.OnSubscribe<User>() {
		@Override
		public void call (Subscriber<? super User> observer) {
			try {
				if (!observer.isUnsubscribed()) {
					restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
					observer.onNext(user);
					observer.onCompleted();
				}
			} catch (Exception e) {
				observer.onError(e);
			}
		}
	});
}
```
&nbsp;&nbsp;��ʹ�� @HystrixCommand ע��ʵ����Ӧʽ����ʱ������ͨ�� observableExecutionMode ������������ʹ�� observe() ���� toObservable() ��ִ�з�ʽ��  
&nbsp;&nbsp;��@HystrixCommand(observableExecutionMode = ObservableExecutionMode.EAGER)��EAGER �Ǹò�����ģʽֵ����ʾʹ�� observe() ִ�з�ʽ��  
&nbsp;&nbsp;��@HystrixCommand(observableExecutionMode = ObservableExecutionMode.LAZY)����ʾʹ�� toObservable() ִ�з�ʽ��  
## ������񽵼�
&nbsp;&nbsp;�� HystrixCommand �п���ͨ����д getFallback() ������ʵ�ַ��񽵼��߼��� Hystrix ���� run() ִ�й����г��ִ��󡢳�ʱ���̳߳ؾܾ�����·���۶ϵ����ʱ��ִ�� getFallback() �����ڵ��߼���  
&nbsp;&nbsp;�� HystrixObservableCommand ʵ�ֵ� Hystrix �����У�ͨ�� resumeWithFallback ������ʵ�ַ��񽵼��߼����÷����᷵��һ�� Observable ���󣬵�����ִ��ʧ�ܵ�ʱ�� Hystrix �Ὣ Observable �еĽ��֪ͨ�����ж����ߡ�  
&nbsp;&nbsp;��Ҫͨ��ע��ʵ�ַ��񽵼�ֻ��Ҫʹ��@HystrixCommand �е� fallbackMethod ������ָ������ķ��񽵼�ʵ�ַ�����  
&nbsp;&nbsp;��ʵ��ʹ��ʱ��������ҪΪ�����ִ�й����п��ܻ�ʧ�ܵ� Hystrix ����ʵ�ַ��񽵼��߼�������Ҳ��һЩ������Բ�ȥʵ�ֽ����߼����磺  
&nbsp;&nbsp;��**ִ��д����������**���� Hystrix ����������ִ��д���������Ƿ���һЩ��Ϣ��ʱ��ͨ�����������Ĳ����ķ��������� void ����Ϊ�յ� Observable ��ʵ�ַ��񽵼������岻�Ǻܴ󡣵�д�����ʧ�ܵ�ʱ������ͬ��ֻ��Ҫ֪ͨ�����߼��ɡ�  
&nbsp;&nbsp;��**ִ������������߼��������**���� Hystrix ����������ִ���������������һ�ݱ�����ǽ����κ����͵����߼���ʱ��ͨ����Щ����ֻ�轫���󴫲��������ߣ�Ȼ���õ������Ժ����Զ����Ƿ��͸�������һ����Ĭ�Ľ���������Ӧ��  
## �쳣����
### �쳣����
&nbsp;&nbsp;�� HystrixCommand ʵ�ֵ� run() �������׳��쳣ʱ������ HystrixBadRequestException ֮�⣬�����쳣���ᱻ Hystrix ��Ϊ����ִ��ʧ�ܲ��������񽵼��Ĵ����߼���  
&nbsp;&nbsp;��ʹ������ʵ�� Hystrix ����ʱ������֧�ֺ���ָ���쳣���͹��ܣ�ֻ��Ҫͨ������@HystrixCommand ע��� ignoreExceptions ������ Hystrix �Ὣָ�����Ե��쳣��װ�� HystrixBadRequestException ���׳��������Ͳ��ᴥ�������� fallback �߼���  
### �쳣��ȡ
&nbsp;&nbsp;���˴�ͳ��ʵ�ַ�ʽ֮�⣬ֻ��Ҫ�� fallback ʵ�ַ����Ĳ��������� Throwable e ����Ķ��壬�Ϳ����ڷ����ڲ��Ϳ��Ի�ȡ�������񽵼��ľ����쳣�����ˡ�  
``` java
@HystrixCommand(fallbackMethod = "fallback1")
User getUserById(String id) {
	throw new RuntimeException("getUserById command failed");
}

User fallback1(String id, Throwable e ) {
	assert "getUserById command failed".equals(e.getMessage());
}
```
### �������ơ������Լ��̳߳ػ���
&nbsp;&nbsp;�Լ̳з�ʽʵ�ֵ� Hystrix ����ʹ��������ΪĬ���������ƣ�ͬʱҲ�����ڹ��캯����ͨ�� Setter ��̬�������ã����磺
``` java
public UserCommand(){   
	super(Setter.withGroupKey(HystrixCommandGroupKey.Factory.asKey("GroupName"))
                .andCommandKey(HystrixCommandKey.Factory.asKey("CommandName")));
}
```
&nbsp;&nbsp;ͨ�����������飬 Hystrix �����������֯��ͳ������ĸ澯���Ǳ��̵���Ϣ��ͬʱ�� Hystrix ����Ĭ�ϵ��̻߳���Ҳ�Ǹ������������ʵ�ֵġ�Ĭ������£� Hystrix ������ͬ����������ʹ��ͬһ���̳߳أ�������Ҫ�ڴ��� Hystrix ����ʱΪ���ƶ�����������ʵ��Ĭ�ϵ��̳߳ػ��֡�  
&nbsp;&nbsp;Ϊ��ʹ Hystrix ���̳߳ط������������ Hystrix ���ṩ�� HystrixThreadPoolKey �����̳߳ؽ������ã�ͨ����ʵ�ָ�ϸ���ȵ��̳߳ػ��֣����磺  
``` java
public UserCommand(){   
	super(Setter.withGroupKey(HystrixCommandGroupKey.Factory.asKey("GroupName"))
                .andCommandKey(HystrixCommandKey.Factory.asKey("CommandName"))
                .andThreadPoolKey(HystrixThreadPoolKey.Factory.asKey("ThreadPoolKey")));
}
```
&nbsp;&nbsp;����ͨ�� HystrixThreadPoolKey �ķ�ʽ��ָ���̳߳صĻ��֣�������ͨ��������Ĭ�Ϸ�ʽʵ�ֻ��֣���Ϊ�����ͬ��������ܴ�ҵ���߼�����������ͬһ���飬����������ʵ�ֱ�������Ҫ������������и��롣  
&nbsp;&nbsp;ʹ�� @HystrixCommand���÷�ʽ��
``` java
@HystrixCommand(commandKey = "getUserById", groupKey = "UserGoup", threadPoolKey = "getUserByIdThread")
User getUserById(String id) {
	return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
}
```
### ���󻺴�
#### �������󻺴湦��
&nbsp;&nbsp;ͨ����д getCacheKey() �������������󻺴档  
``` java
@Override
protected String getCacheKey() {
}
```
&nbsp;&nbsp;ͨ���� getCacheKey �����з��ص����󻺴� key ֵ��ʹ�ø�����߱��˻��湦�ܡ�����ͬ���ⲿ�������߼�������ͬһ����������ʱ�� Hystrix ����� getCacheKey �������ص�ֵ�������Ƿ����ظ���������� cacheKey ��ͬ����ô����������ֻ���ڵ�һ�����󵽴�ʱ����ʵ�ص���һ�Σ�����������ֱ�Ӵ����󻺴��з��ؽ�������󻺴��� run() �� construct() ִ��֮ǰ��Ч�����Լ��ٲ���Ҫ���߳̿�����  
#### ����ʧЧ���湦��
&nbsp;&nbsp;��������������и������ݵ�д��������ô�����е����ݾ���Ҫ�ڽ���д����ʱ���м�ʱ�����Է�ֹ�����������������ȡ��ʧЧ�����ݡ�  
&nbsp;&nbsp;ͨ�� HystrixRequestCache.clear() �������л��������  
``` java
public class UserGetCommand extends HystrixCommand<User> {

    private static final HystrixCommandKey GETTER_KEY = HystrixCommandKey.Factory.asKey("CommandKey");
    private RestTemplate restTemplate;
    private Long id;

    public UserGetCommand(RestTemplate restTemplate, Long id) {
        super(Setter.withGroupKey(HystrixCommandGroupKey.Factory.asKey("GetSetGet")));
        this.restTemplate = restTemplate;
        this.id = id;
    }

    @Override
    protected User run() throws Exception {
        return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
    }

    @Override
    protected String getCacheKey() {
        // ���� id ���뻺��
        return String.valueOf(id);
    }

    public static void flushCache(Long id) {
        // ˢ�»��棬���� id ��������
        HystrixRequestCache.getInstance(GETTER_KEY, HystrixConcurrencyStrategyDefault.getInstance())
                .clear(String.valueOf(id));
    }
}
```
&nbsp;&nbsp;HystrixRequestCache.getInstance(GETTER_KEY, HystrixConcurrencyStrategyDefault.getInstance()) ������Ĭ�ϵ� Hystrix ���������и��� GETTER_KEY ��ȡ������������󻺴���� HystrixRequestCache ��ʵ����Ȼ���ٵ��ø����󻺴����ʵ���� clear �������� Key Ϊ���� User �� id ֵ�Ļ������ݽ�������  
#### ʹ��ע��ʵ�����󻺴�
&nbsp;&nbsp; Hystrix �ṩ��ר�������󻺴��ע�⡣  
| ע�� | ����         | ���� |
| ------------ | --------------- | ----- |
| @CacheResult | ��ע�����������������صĽ��Ӧ�ñ����棬��������@HystrixCommand ע����ʹ�� | cacheKeyMethod |
| @CacheRemove | ��ע����������������Ļ���ʧЧ��ʧЧ�Ļ�����ݶ���� Key ���� | commandKey, cacheKeyMethod |
| @CacheKey | ��ע����������������Ĳ����ϱ�ǣ�ʹ����Ϊ����� Key ֵ�����û�б�ע���ʹ�����в��������ͬʱ��ʹ���� @CacheResult �� @CacheRemove ע��� cacheKeyMethod ����ָ������ Key �����ɣ���ô��ע�⽫�������� | value |

&nbsp;&nbsp;��**�������󻺴�**�� Hystrix  �Ὣ���ؽ���������󻺴��У������Ļ��� Key ֵ��ʹ�����еĲ�����Ҳ�������� Long ���͵� id ֵ��  
``` java
@CacheResult
@HystrixCommand
public User getUserById(String id) {
		return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
}
```
&nbsp;&nbsp;��**���建�� Key**������ʹ�� @CacheResult �� @CacheRemove ע��� cacheKeyMethod ������ָ����������ɺ�����Ҳ����ͨ��ʹ�� @CacheKey ע���ڷ���������ָ��������װ���� Key ��Ԫ�ء�  
``` java
@CacheResult(cacheKeyMethod = "getUserByIdCacheKey")
@HystrixCommand
public User getUserById(Long id) {
		return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
}

private Long getUserByIdCacheKey(Long id) {
	return id;
}
```
&nbsp;&nbsp;@CacheKey ע������ȼ��� cacheKeyMethod �����ȼ��ͣ�����Ѿ�ʹ���� cacheKeyMethod ָ������ Key �����ɺ�������ô @CacheKey ע�ⲻ����Ч��  
``` java
@CacheResult
@HystrixCommand
public User getUserById(@CacheKey("id") Long id) {
		return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
}
```
&nbsp;&nbsp; @CacheKey ע����˿���ָ������������Ϊ���� Key ֮�⣬��������ʲ���������ڲ�������Ϊ���� Key ������ʾ����ָ���� User ����� id ������Ϊ���� Key��  
``` java
@CacheResult
@HystrixCommand
public User getUserById(@CacheKey("id") User user) {
		return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, user.getId());
}
```
&nbsp;&nbsp;��**��������**���� Hystrix ��ע�������У�����ͨ�� @CacheRemove ע����ʵ��ʧЧ���������ʾ�����£�
``` java
@CacheResult
@HystrixCommand
public User getUserById(@CacheKey("id") Long id) {
		return restTemplate.getForObject("http://USER-SERVICE/users/{1}", User.class, id);
}

@CacheRemove(commandKey = "getUserById")
@HystrixCommand
public void update(@CacheKey("id") User user) {
		return restTemplate.postForObject("http://USER-SERVICE/users", User.class);
}
```
&nbsp;&nbsp; @CacheRemove ע��� commandKey �����Ǳ���Ҫָ���ģ�����ָ����Ҫʹ�����󻺴�����������Ϊֻ��ͨ�������Ե����ã� Hystrix �����ҵ���ȷ�����������λ�á�  
### ����ϲ�
&nbsp;&nbsp; ΢�������е�����ͨ��ͨ��Զ�̵���ʵ�֣���Զ�̵�����������������ͨ��������������ռ�á��ڸ߲���������£���ͨ�Ŵ��������ӣ��ܵ�ͨ�����Ľ����ò����롣ͬʱ����������������̳߳���Դ���ޣ��������Ŷӵȴ�����Ӧ�ӳٵ������Ϊ���Ż����������⣬ Hystrix �ṩ�� HystrixCollapser ��ʵ������ĺϲ����Լ���ͨ�����ĵ��߳�����ռ�á�  
&nbsp;&nbsp;  HystrixCollapser ʵ������ HystrixCommand ֮ǰ��ֹһ���ϲ���������������һ���̵ܶ�ʱ�䴰��Ĭ��10���룩�ڶ�ͬһ��������Ķ������������ϲ���������ʽ��������Ĺ��ܣ������ṩ��Ҳ��Ҫ�ṩ��Ӧ������ʾ�нӿڣ���ͨ�� HystrixCollapser �ķ�װ�������߲���Ҫ��ע�̺߳ϲ���ϸ�ڹ��̣�ֻ��Ҫ��ע����������ʹ���  

?	��ʹ�� HystrixCollapser ����ϲ���֮���߳�ռ���������ͼ����������Դ��Ч���Ҷ�ʱ���ڻ�����߲��������ʱ��Ϊ�������Ӳ����ö�������ӳٿ��Կ���ʹ������ϲ����ķ�ʽ��������Ż���

![](HystrixCommand.png)
#### ����ϲ��Ķ��⿪��

- **�����������ӳ١�**�����������������������һ�����ӳٵ������ô�ӳ�ʱ�䴰��ʱ�����ľ��Ե�΢������ˡ�
- **�ӳ�ʱ�䴰�ڵĲ�������**���һ��ʱ�䴰�ھ��кܸߵĲ����������ҷ����ṩ��Ҳʵ������������ӿڣ���ôʹ������ϲ���������Ч��������������������������ϵͳ����������ʱ�ӳ�ʱ�䴰�����ӵ����ľͿ��Ժ��Բ����ˡ�

### �������

?	HystrixPropertiesStrategy ʵ�ֵĸ�����������4�����ȼ���

- **ȫ��Ĭ��ֵ**

- **ȫ����������**

- **ʵ��Ĭ��ֵ**

- **ʵ����������**
#### Command ����

##### execution ����

?	execution ���ÿ��Ƶ��� HystrixCommand.run() ��ִ�С�

- execution.isolation.strategy���������������� HystrixCommand.run() ִ�еĸ�����ԡ�
- execution.isolation.thread.timeoutInMilliseconds���������������� HystrixCommand ִ�еĳ�ʱʱ�䣬��λΪ���롣�� HystrixCommand ִ��ʱ�䳬��������ֵ֮�� Hystrix �Ὣ��ִ��������Ϊ TIMEOUT ��������񽵼������߼���
- execution.timeout.enabled���������������� HystrixCommand.run() ��ִ���Ƿ����ó�ʱʱ�䡣Ĭ��Ϊ true ���������Ϊ false �� ��ô execution.isolation.thread.timeoutInMilliseconds ���Ե����ý����������á�
- execution.isolation.thread.interruptOnTimeout���������������õ� HystrixCommand.run() ִ�г�ʱ��ʱ���Ƿ�Ҫ�����жϡ�
- execution.isolation.thread.interruptOnCancel���������������� HystrixCommand.run() ִ�б�ȡ����ʱ���Ƿ�Ҫ�����жϡ�
- execution.isolation.semaphore.maxConcurrentRequests���� HystrixCommand �ĸ������ʹ���ź�����ʱ�򣬸��������������ź����Ĵ�С��������������������󲢷��������ﵽ������ֵʱ�����������󽫻ᱻ�ܾ���

##### fallback ����

?	������Щ������������ HystrixCommand.getFallback() ��ִ�С���Щ����ͬʱ�������̳߳ص��ź����ĸ�����ԡ�

- fallback.isolation.semaphore.maxConcurrentRequests���������������ôӵ����߳������� HystrixCommand.getFallback() ����ִ�е���󲢷������������ﵽ��󲢷�������ʱ�����������󽫻ᱻ�ܾ����׳��쳣����Ϊ���Ѿ�û�к����� fallback ���Ա������ˣ���
- fallback.enabled���������������÷��񽵼������Ƿ����ã��������Ϊ false ����ô������ʧ�ܻ��߾ܾ�����ʱ����������� HystrixCommand.getFallback() ��ִ�з��񽵼��߼���

##### circuitBreaker ����

?	������Щ�Ƕ�·�����������ã��������� HystrixCircuitBreaker ����Ϊ��

- circuitBreaker.enabled������������ȷ������������ʧ��ʱ���Ƿ�ʹ�ö�·���������佡��ָ��Ͷ�·����
- circuitBreaker.requestVolumeThreshold�����������������ڹ���ʱ�䴰�У���·���۶ϵ���С������������Ĭ��ֵΪ20��ʱ���������ʱ�䴰��Ĭ��10�룩�ڽ��յ���19�����󣬼�ʹ��19������ʧ���ˣ���·��Ҳ����򿪡�
- circuitBreaker.sleepWindowInMilliseconds���������������õ���·����֮�������ʱ�䴰������ʱ�䴰����֮�󣬻Ὣ��·����Ϊ���뿪��״̬�������۶ϵ�������������Ȼʧ�ܾͽ���·����������Ϊ���򿪡�״̬������ɹ�������Ϊ���رա�״̬��
- circuitBreaker.errorThresholdPercentage���������������ö�·���򿪵Ĵ���ٷֱ����������磬Ĭ��ֵΪ5000������£���ʾ�ڹ���ʱ�䴰�У��������������� circuitBreaker.errorThresholdPercentage ��ֵ��ǰ���£���������������İٷֱȳ���50���ͰѶ�·������Ϊ���򿪡�״̬�����������Ϊ���رա�״̬��
- circuitBreaker.forceOpen�����������������Ϊ true ����·����ǿ�ƽ��롰�򿪡�״̬������ܾ��������󡣸����������� circuitBreaker.forceClosed ���ԡ�
- circuitBreaker.forceClosed �����������������Ϊ true ����·����ǿ�ƽ��롰�رա�״̬�����������������

##### metrics ����

?	��������Ծ��� HystrixCommand �� HystrixObservableCommand ִ���в����ָ����Ϣ�йء�

- metrics.rollingStats.timeInMilliseconds���������������ù���ʱ�䴰�ĳ��ȣ���λΪ���롣��ʱ�����ڶ�·���жϽ�����ʱ��Ҫ�ռ���Ϣ�ĳ���ʱ�䡣��·�����ռ�ָ����Ϣ��ʱ���������õ�ʱ�䴰���Ȳ�ֳɶ����Ͱ�����ۼƸ�����ֵ��ÿ����Ͱ����¼��һ��ʱ���ڵĲɼ�ָ�ꡣ���磬������Ĭ��ֵ10000����ʱ����·��Ĭ�Ͻ����ֳ�10��Ͱ��Ͱ������Ҳ����ͨ�� metrics.rollingStats.numBuckets �������ã���ÿ��Ͱ��¼1000�����ڵ�ָ����Ϣ��

``` ע�⣺�����Դ� Hystrix1.4.12�汾��ʼ��Brixton.SR5 �汾��ʹ����1.5.3�汾����ֻ����Ӧ�ó�ʼ����ʱ����Ч��ͨ����̬ˢ�����ò������Ч������������Ϊ�˱�����������ڼ�����ݶ�ʧ������� ```

- metrics.rollingStats.numBuckets���������������ù���ʱ�䴰ͳ��ָ����Ϣʱ���֡�Ͱ����������

``` ע�⣺metrics.rollingStats.timeInMilliseconds ���������ñ����ܹ��� metrics.rollingStats.numBuckets ������������Ȼ���׳��쳣���ò����� metrics.rollingStats.timeInMilliseconds һ������ Hystrix1.4.12�汾��ʼ��Brixton.SR5 �汾��ʹ����1.5.3�汾����ֻ����Ӧ�ó�ʼ����ʱ����Ч��ͨ����̬ˢ�����ò������Ч������������Ϊ�˱�����������ڼ�����ݶ�ʧ�������```

- metrics.rollingPercentile.enabled���������������ö�����ִ�е��ӳ��Ƿ�ʹ�ðٷ�λ�������ٺͼ��㡣�������Ϊ false �� ��ô���еĸ�Ҫͳ�ƶ�������-1��
- metrics.rollingPercentile.timeInMilliseconds���������������ðٷ�λͳ�ƵĹ������ڵĳ���ʱ�䣬��λΪ���롣

``` ע�⣺�����Դ� Hystrix1.4.12�汾��ʼ��Brixton.SR5 �汾��ʹ����1.5.3�汾����ֻ����Ӧ�ó�ʼ����ʱ����Ч��ͨ����̬ˢ�����ò������Ч������������Ϊ�˱�����������ڼ�����ݶ�ʧ������� ```

- metrics.rollingPercentile.timeInMilliseconds���������������ðٷ�λͳ�ƹ���������ʹ�á�Ͱ����������

``` ע�⣺metrics.rollingPercentile.timeInMilliseconds ���������ñ����ܹ��� metrics.rollingPercentile.numBuckets ������������Ȼ���׳��쳣���ò����� metrics.rollingStats.timeInMilliseconds һ������ Hystrix1.4.12�汾��ʼ��Brixton.SR5 �汾��ʹ����1.5.3�汾����ֻ����Ӧ�ó�ʼ����ʱ����Ч��ͨ����̬ˢ�����ò������Ч������������Ϊ�˱�����������ڼ�����ݶ�ʧ�������```

- metrics.rollingPercentile.bucketSize������������������ִ�й�����ÿ����Ͱ���б��������ִ�д���������ڹ���ʱ�䴰�ڷ����������趨ֵ��ִ�д������ʹ������λ�ÿ�ʼ��д�����磬����ֵ����Ϊ100����������Ϊ10�룬����10����һ����Ͱ��������500��ִ�У���ô�á�Ͱ����ֻ�������100��ִ�е�ͳ�ơ����⣬���Ӹ�ֵ�Ĵ�С���������ڴ�����ģ�����������ٷ�λ������ļ���ʱ�䡣

``` ע�⣺�����Դ� Hystrix1.4.12�汾��ʼ��Brixton.SR5 �汾��ʹ����1.5.3�汾����ֻ����Ӧ�ó�ʼ����ʱ����Ч��ͨ����̬ˢ�����ò������Ч������������Ϊ�˱�����������ڼ�����ݶ�ʧ������� ```

##### requestContext ����

?	����������漰 HystrixCommand ʹ�õ� HystrixRequestContext �����á�

- requestCache.enabled�����������������Ƿ������󻺴档
- requestLog.enabled���������������� HystrixCommand ��ִ�к��¼��Ƿ��ӡ��־�� HystrixRequestLog �С�

#### collapser ����

?	������������ϲ���ص���Ϊ��

- maxRequestsInBatch���ò�����������һ������ϲ�������������������������
- timerDelayInMilliseconds���ò����������������������ÿ�������ӳٵ�ʱ�䣬��λΪ���롣
- requestCache.enabled���ò�����������������������Ƿ������󻺴档

#### threadPool ����

?	����������������� Hystrix �����������̳߳ص����á�

- coreSize���ò�����������ִ�������̳߳صĺ����߳�������ֵҲ��������ִ�е���󲢷�����
- maxQueueSize���ò������������̳߳ص������д�С��������Ϊ-1ʱ���̳߳ؽ�ʹ�� SynchronousQueue ʵ�ֶ��У�����ʹ�� LinkedBlockingQueue ʵ�ֵĶ��С�

``` ע�⣺������ֻ����Ӧ�ó�ʼ����ʱ����Ч���޷�ͨ����̬ˢ�µķ�ʽ�������� ```

- queueSizeRejectionThreshold���ò�������Ϊ�������þܾ���ֵ��ͨ���ò�������ʹ����û�дﵽ���ֵҲ�ܾܾ����󡣸ò�����Ҫ�Ƕ� LinkedBlockingQueue ���еĲ��䣬��Ϊ LinkedBlockingQueue ���в��ܶ�̬�޸����Ķ����С����ͨ�������ԾͿ��Ե����ܾ�����Ķ��д�С�ˡ�

``` ע�⣺�� maxQueue ����Ϊ-1��ʱ�򣬸����Բ�����Ч�� ```