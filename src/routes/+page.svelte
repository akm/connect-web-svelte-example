<script lang="ts">
    import { createPromiseClient } from "@connectrpc/connect";
    import { createConnectTransport } from "@connectrpc/connect-web";

    // Import service definition that you want to connect to.
    import { ElizaService } from "@buf/connectrpc_eliza.connectrpc_es/connectrpc/eliza/v1/eliza_connect";

    // The transport defines what type of endpoint we're hitting.
    // In our example we'll be communicating with a Connect endpoint.
    // If your endpoint only supports gRPC-web, make sure to use
    // `createGrpcWebTransport` instead.
    const transport = createConnectTransport({
    baseUrl: "https://demo.connectrpc.com",
    });

    // Here we make the client itself, combining the service
    // definition with the transport.
    const client = createPromiseClient(ElizaService, transport);

    let inputValue = '';

    type Message = {
        fromMe: boolean;
        message: string;
    };
    let messages: Message[] = [];
</script>

<form on:submit={async (e) => {
    const response = await client.say({sentence: inputValue});
    messages = [
        ...messages,
        {fromMe: true, message: inputValue},
        {fromMe: false, message: response.sentence},
    ];
    inputValue = '';
}}>
    <input bind:value={inputValue}/>
    <button type="submit">Send</button>
</form>
