<script lang="ts">
  import { addChat, clearChats } from "./Storage.svelte";
  import type { Chat } from "./Types.svelte";

  export let activeChatId: number;
  export let sortedChats: Chat[];
  export let apiKey: string;
</script>

<aside class="menu">
  <p class="menu-label">Chats</p>
  <ul class="menu-list">
    {#if sortedChats.length === 0}
      <li><a class="panel-block" href={"#"}>No chats yet...</a></li>
    {:else}
      <li>
        <ul>
          {#each sortedChats as chat}
            <li>
              <a
                href={"#"}
                class="panel-block"
                class:is-disabled={!apiKey}
                class:has-background-light={activeChatId === chat.id}
                on:click|preventDefault={() => (activeChatId = chat.id)}>{chat.name || `Chat ${chat.id}`}</a
              >
            </li>
          {/each}
        </ul>
      </li>
    {/if}
  </ul>
  <p class="menu-label">Actions</p>
  <ul class="menu-list">
    <li>
      <a
        href={"#"}
        class="panel-block"
        class:is-disabled={!apiKey}
        class:has-background-light={!activeChatId}
        on:click|preventDefault={() => {
          activeChatId = null;
        }}><span class="greyscale mr-2">🔑</span> API key</a
      >
    </li>
    <li>
      <a
        href={"#"}
        class="panel-block"
        class:is-disabled={!apiKey}
        on:click|preventDefault={() => {
          activeChatId = addChat();
        }}><span class="greyscale mr-2">➕</span> New chat</a
      >
    </li>
    <li>
      <a
        href={"#"}
        class="panel-block"
        class:is-disabled={!apiKey}
        on:click|preventDefault={() => {
          clearChats();
          activeChatId = null;
        }}><span class="greyscale mr-2">🗑️</span> Clear chats</a
      >
    </li>
  </ul>
</aside>
