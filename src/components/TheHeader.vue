<template>
  <header class="flex justify-between border-b border-slate-300 px-8 py-8">
    <div class="flex items-center gap-4">
      <img
        src="D:\React Projects\vue-sneaker-site-project\public\img\logo.png"
        alt="Logo"
        class="w-10"
      />
      <div>
        <h2 class="text-xl font-bold uppercase">Vue Sneakers</h2>
        <p class="text-slate-400 italic">The best place to buy sneakers</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li class="flex items-center gap-3 text-gray-600 hover:text-black cursor-pointer">
        <img src="D:\React Projects\vue-sneaker-site-project\public\img\cart.svg" alt="Cart" />
        <b>$55</b>
      </li>

      <li class="flex items-center gap-3 text-gray-600 hover:text-black cursor-pointer">
        <img src="D:\React Projects\vue-sneaker-site-project\public\img\heart.svg" alt="Saved" />
        <span>Saved</span>
      </li>

      <li class="flex items-center gap-3 text-gray-600 hover:text-black cursor-pointer">
        <img src="D:\React Projects\vue-sneaker-site-project\public\img\user.svg" alt="Profile" />
        <span>Profile</span>
      </li>
    </ul>
  </header>
</template>
