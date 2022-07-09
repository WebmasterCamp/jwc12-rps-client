<script>
  import { io } from "socket.io-client";
  const socket = io("ws://localhost:8080", { transports: ["websocket"] });
  console.log(socket);
  socket.on("portal", (arg) => {
    console.log(arg);
  });

  const resolve = (result) => {
    socket.emit("result", result);
  };
</script>

<main class="flex w-[100vw] h-[100vh] justify-center items-center">
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
</main>

<style>
  .btn {
    @apply text-6xl p-2 m-3 sm:m-4 rounded-lg bg-slate-100 border border-slate-300;
  }
</style>
