<script lang="ts">
    import {Button} from "$lib/components/ui/button";
    import * as Card from "$lib/components/ui/card";
    import {Input} from "$lib/components/ui/input";
    import {Badge} from "$lib/components/ui/badge";

    let resourceName = $state("");
    let resources = $state<Record<number, string>>({});
    let id = $state(0);
    function addResource() {
        if (!resourceName.trim()) return;
        resources[id] = resourceName.trim();
        resourceName = "";
        id++;
        inc();
    }

    let c = $state(0);

    function inc() {
        c++
    }

</script>

<main class="m-auto max-w-3xl p-8">
    <h1 class="mb-3 text-5xl font-bold">BriefBoard</h1>

    <Card.Root>
        <Card.Header>
            <Card.Title>Team Knowledge Base</Card.Title>
            <Card.Description>
                Organize and summarize learning resources.
            </Card.Description>
        </Card.Header>

        <Card.Content>
            <div class="flex gap-2">
                <Input
                        placeholder="Resource title..."
                        bind:value={resourceName}
                />
                <Button onclick={addResource}>
                    Add resource
                </Button>
            </div>
        </Card.Content>
    </Card.Root>

    {#each Object.entries(resources).reverse() as [id, resource] (id)}
        <Card.Root class="my-auto">
            <Card.Header>
                <Card.Title>Tasks {id}</Card.Title>
            </Card.Header>
            <Card.Content>
                <div class="mt-6 space-y-3">

                    <div class="flex items-center justify-between rounded-lg border p-4">
                        <span>{resource}</span>
                        <Badge variant="secondary">New</Badge>
                    </div>
                </div>
            </Card.Content>
        </Card.Root>
    {/each}

</main>
