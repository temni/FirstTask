Console Example
===============

This is a simple example that shows how to get started with Camel.

You will need to compile this example first:
  mvn compile

To run the example type
  mvn camel:run

This is first task solution. It uses text files input (see in.A directory) instead of MQ - for more convinient testing (otherwise you need to have AcitveMQ installed and configured with appropriate Queues)



For change the approach from text files to MQ just edit camel spring xml config (src/main/resources/META-INF/spring/camel-context.xml):

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route autoStartup="
      <from uri="file://in.A"/>
      <choice>
      <when>
        <xpath>/msg/to/text()='B'</xpath>
        <to uri="file://out.B/"/>
      </when>
      <otherwise>
        <to uri="file://out.C/"/>
      </otherwise>
      </choice>
    </route>
</camelContext>

TO

<camelContext xmlns="http://camel.apache.org/schema/spring">
    <route autoStartup="
      <from uri="activemq:in.A"/>
      <choice>
      <when>
        <xpath>/msg/to/text()='B'</xpath>
        <to uri="activemq:out.B"/>
      </when>
      <otherwise>
        <to uri="activemq:out.C"/>
      </otherwise>
      </choice>
    </route>
</camelContext>


11.07.2014 Kirichenko Evgeniy for LiveTex company. 15:09 MSK
