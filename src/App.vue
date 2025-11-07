<template>
  <div id="app" class="min-h-screen relative overflow-hidden flex flex-col bg-slate-50">
    <!-- Subtle Background -->
    <div class="fixed inset-0 -z-10">
      <div class="absolute inset-0 bg-gradient-to-br from-slate-50 via-white to-slate-100"></div>
      <div class="absolute top-0 right-0 w-[500px] h-[500px] bg-indigo-100/40 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob"></div>
      <div class="absolute bottom-0 left-0 w-[500px] h-[500px] bg-slate-200/40 rounded-full mix-blend-multiply filter blur-3xl opacity-70 animate-blob animation-delay-2000"></div>
    </div>

    <!-- Clean Header -->
    <header class="w-full border-b border-slate-200 bg-white/80 backdrop-blur-xl shadow-sm sticky top-0 z-50">
      <div class="mx-auto max-w-7xl px-4 sm:px-6 py-4 flex items-center justify-between">
        <div class="flex items-center gap-3 group cursor-pointer">
          <div class="h-11 w-11 rounded-xl bg-gradient-to-br from-indigo-600 to-indigo-700 text-white flex items-center justify-center font-bold text-lg shadow-lg shadow-indigo-200 group-hover:shadow-xl group-hover:shadow-indigo-300 transition-all duration-300 group-hover:scale-105">
            J
          </div>
          <div class="text-left">
            <h1 class="text-xl font-bold text-slate-900">QR Code Generator</h1>
            <p class="text-xs text-slate-500 font-medium">by JCode</p>
          </div>
        </div>
        <nav class="hidden sm:flex items-center gap-4 text-sm font-medium">
          <a href="/" class="text-slate-600 hover:text-indigo-600 transition-colors duration-200 px-3 py-2">Home</a>
          <a href="https://jcode.be" target="_blank" rel="noopener" class="px-5 py-2.5 rounded-lg bg-indigo-600 hover:bg-indigo-700 text-white shadow-md hover:shadow-lg hover:shadow-indigo-200 transition-all duration-200 hover:scale-105">
            Bezoek JCode
          </a>
        </nav>
      </div>
    </header>

    <main class="flex-1 mx-auto w-full max-w-7xl px-4 sm:px-6 py-12">
      <router-view />
    </main>

    <!-- Clean Footer -->
    <footer class="w-full border-t border-slate-200 bg-white/80 backdrop-blur-xl">
      <div class="mx-auto max-w-7xl px-4 sm:px-6 py-8 text-center">
        <div class="mb-3">
          <div class="inline-flex items-center gap-2 text-sm font-medium text-slate-600">
            <span>Gemaakt met</span>
            <svg class="w-5 h-5 text-red-500 animate-heartbeat" fill="currentColor" viewBox="0 0 20 20">
              <path fill-rule="evenodd" d="M3.172 5.172a4 4 0 015.656 0L10 6.343l1.172-1.171a4 4 0 115.656 5.656L10 17.657l-6.828-6.829a4 4 0 010-5.656z" clip-rule="evenodd"></path>
            </svg>
            <span>door JCode</span>
          </div>
        </div>
        <p class="text-sm text-slate-500">© {{ new Date().getFullYear() }} JCode. Alle rechten voorbehouden.</p>
      </div>
    </footer>
  </div>
  
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');

#app {
  font-family: 'Inter', -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

* {
  box-sizing: border-box;
}

/* Blob animations for background */
@keyframes blob {
  0% {
    transform: translate(0px, 0px) scale(1);
  }
  33% {
    transform: translate(30px, -50px) scale(1.1);
  }
  66% {
    transform: translate(-20px, 20px) scale(0.9);
  }
  100% {
    transform: translate(0px, 0px) scale(1);
  }
}

.animate-blob {
  animation: blob 7s infinite;
}

.animation-delay-2000 {
  animation-delay: 2s;
}

.animation-delay-4000 {
  animation-delay: 4s;
}

/* Heartbeat animation */
@keyframes heartbeat {
  0%, 100% {
    transform: scale(1);
  }
  10%, 30% {
    transform: scale(0.9);
  }
  20%, 40%, 50%, 60%, 70% {
    transform: scale(1.1);
  }
  80% {
    transform: scale(1.05);
  }
  90% {
    transform: scale(1);
  }
}

.animate-heartbeat {
  animation: heartbeat 2s ease-in-out infinite;
}

/* Smooth scrollbar */
::-webkit-scrollbar {
  width: 10px;
}

::-webkit-scrollbar-track {
  background: rgba(255, 255, 255, 0.1);
}

::-webkit-scrollbar-thumb {
  background: rgba(255, 255, 255, 0.3);
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: rgba(255, 255, 255, 0.5);
}
</style>
