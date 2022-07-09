<script>
  import { io } from "socket.io-client";
  import { onMount } from "svelte";
  import { Router, Link, Route, navigate } from "svelte-navigator";
  const socket = io(
    "https://9d48-2001-44c8-428c-82d6-b077-bd9b-34af-5647.ap.ngrok.io",
    { transports: ["websocket"] }
  );

  let isConnect = true;

  console.log(socket);
  socket.on("connect", (arg) => {
    socket.emit("portal", socket.id);
    console.log(arg);
  });

  socket.on("status", (arg) => {
    if (socket.id !== arg) {
      isConnect = false;
    }
  });

  const resolve = (result) => {
    socket.emit("result", result);
  };

  const resolveShit = (result) => {
    socket.emit("shit", result);
  };

  onMount(() => {
    window.addEventListener("keydown", (e) => {
      if ((e.key === "F" || e.key === "f") && e.metaKey) {
        navigate("/tofu-eating-cat");
      }
    });
  });
</script>

<Router>
  <Route path="/">
    <main class="flex w-[100vw] h-[100vh] justify-center items-center">
      {#if isConnect}
        <div class="flex flex-wrap">
          <div class="w-full flex justify-center items-center">
            <button
              on:click={() => {
                resolve("🪨");
              }}
              class="btn">🪨</button
            >
            <button
              on:click={() => {
                resolve("📄");
              }}
              class="btn">📄</button
            >
          </div>
          <div class="flex w-full justify-center items-center">
            <button
              on:click={() => {
                resolve("✂️");
              }}
              class="btn">✂️</button
            >
          </div>
        </div>
      {:else}
        <h1 class="text-4xl">Disconnected</h1>
      {/if}
    </main>
  </Route>
  <Route path="/tofu-eating-cat">
    <button
      class="text-8xl p-2 border-2"
      on:click={() => {
        resolveShit("win");
      }}>🏆</button
    >
    <button
      class="text-8xl p-2 border-2"
      on:click={() => {
        resolveShit("lose");
      }}>🥲</button
    >
    <button
      class="text-8xl p-2 border-2"
      on:click={() => {
        resolveShit("normal");
      }}>😀</button
    >
  </Route>
</Router>

<style>
  .btn {
    @apply text-6xl p-2 m-3 sm:m-4 rounded-lg bg-slate-100 border border-slate-300;
  }
</style>
