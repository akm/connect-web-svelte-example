<script type="ts">
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
</script>

<h1>Welcome to SvelteKit</h1>
<p>Visit <a href="https://kit.svelte.dev">kit.svelte.dev</a> to read the documentation</p>
