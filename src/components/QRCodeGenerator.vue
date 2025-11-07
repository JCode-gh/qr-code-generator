<template>
    <div class="qr-code-generator">
        <!-- Hero Section -->
        <div class="text-center mb-12 animate-fade-in-down">
            <div class="relative inline-block mb-6">
                <div class="inline-flex items-center justify-center w-20 h-20 rounded-2xl bg-gradient-to-br from-indigo-600 to-indigo-700 text-white shadow-xl shadow-indigo-200 hover:scale-110 transition-all duration-300 cursor-pointer">
                    <svg class="w-11 h-11" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M12 4v1m6 11h2m-6 0h-2v4m0-11v3m0 0h.01M12 12h4.01M16 20h4M4 12h4m12 0h.01M5 8h2a1 1 0 001-1V5a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1zm12 0h2a1 1 0 001-1V5a1 1 0 00-1-1h-2a1 1 0 00-1 1v2a1 1 0 001 1zM5 20h2a1 1 0 001-1v-2a1 1 0 00-1-1H5a1 1 0 00-1 1v2a1 1 0 001 1z"></path>
                    </svg>
                </div>
            </div>
            <h2 class="text-4xl sm:text-5xl font-bold text-slate-900 mb-3 tracking-tight">
                Maak je QR Code
            </h2>
            <p class="text-slate-600 text-lg font-medium">Genereer professionele QR codes in seconden</p>
        </div>

        <!-- Generator Card -->
        <div class="mx-auto max-w-3xl mb-20 animate-slide-up">
            <div class="relative group">
                <!-- Subtle glow -->
                <div class="absolute -inset-0.5 bg-gradient-to-r from-indigo-600 to-indigo-500 rounded-2xl blur opacity-20 group-hover:opacity-30 transition duration-300"></div>
                
                <div class="relative bg-white rounded-2xl border border-slate-200 p-8 sm:p-10 shadow-xl hover:shadow-2xl transition-all duration-300">
                    <div class="mb-8">
                        <label class="block text-sm font-bold text-slate-700 mb-3 uppercase tracking-wide">
                            <span class="flex items-center gap-2">
                                <svg class="w-5 h-5 text-indigo-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M13.828 10.172a4 4 0 00-5.656 0l-4 4a4 4 0 105.656 5.656l1.102-1.101m-.758-4.899a4 4 0 005.656 0l4-4a4 4 0 00-5.656-5.656l-1.1 1.1"></path>
                                </svg>
                                Jouw URL of Tekst
                            </span>
                        </label>
                        <div class="relative">
                            <input
                                class="block w-full rounded-xl border-0 py-4 px-5 text-slate-900 placeholder:text-slate-400 bg-slate-50 ring-2 ring-slate-200 focus:ring-indigo-600 focus:bg-white sm:text-base transition-all duration-200 hover:ring-slate-300 font-medium"
                                v-model="url" 
                                placeholder="https://jcode.be of jouw gewenste tekst..." 
                                type="text" 
                                @keydown.enter="generateQRCode()" 
                            />
                            <div v-if="url" class="absolute right-4 top-1/2 -translate-y-1/2 px-3 py-1 bg-slate-200 rounded-lg text-slate-600 text-sm font-semibold">
                                {{ url.length }}/1033
                            </div>
                        </div>
                    </div>

                    <div v-if="url.length > 1033" class="mb-6 p-4 bg-red-50 border-l-4 border-red-500 rounded-xl animate-shake-horizontal">
                        <div class="flex items-center gap-3">
                            <svg class="w-5 h-5 text-red-500" fill="currentColor" viewBox="0 0 20 20">
                                <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd"></path>
                            </svg>
                            <span class="text-sm font-semibold text-red-800">De link is te lang (max 1033 karakters)</span>
                        </div>
                    </div>

                    <button 
                        class="w-full bg-gradient-to-r from-indigo-600 to-indigo-700 hover:from-indigo-700 hover:to-indigo-800 text-white font-bold py-4 px-8 rounded-xl shadow-lg shadow-indigo-200 hover:shadow-xl hover:shadow-indigo-300 transition-all duration-200 transform hover:scale-[1.02] active:scale-[0.98] disabled:opacity-50 disabled:cursor-not-allowed disabled:hover:scale-100"
                        @click="generateQRCode"
                        :disabled="!url || url.length > 1033"
                    >
                        <span class="flex items-center justify-center gap-2 text-base">
                            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M13 10V3L4 14h7v7l9-11h-7z"></path>
                            </svg>
                            Genereer QR Code
                        </span>
                    </button>

                    <div v-if="qrCodeDataUrl" class="mt-10 p-8 bg-slate-50 rounded-2xl animate-scale-in">
                        <div class="text-center">
                            <div class="inline-block p-6 bg-white rounded-2xl shadow-lg mb-6 hover:scale-105 transition-transform duration-300">
                                <img :src="qrCodeDataUrl" alt="Generated QR Code" class="qrcode-large mx-auto" />
                            </div>
                            <button 
                                class="inline-flex items-center gap-2 bg-gradient-to-r from-green-600 to-emerald-600 hover:from-green-700 hover:to-emerald-700 text-white font-bold py-3.5 px-8 rounded-xl shadow-lg shadow-green-200 hover:shadow-xl hover:shadow-green-300 transition-all duration-200 transform hover:scale-105 active:scale-95"
                                @click="downloadImage"
                            >
                                <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                                </svg>
                                Download QR Code
                            </button>
                        </div>
                    </div>
                </div>
            </div>
        </div>

        <!-- History Section -->
        <div v-if="savedQRs.length > 0" class="animate-fade-in">
            <div class="text-center mb-10">
                <h3 class="text-3xl sm:text-4xl font-bold text-slate-900 mb-2">Geschiedenis</h3>
                <p class="text-slate-600 text-lg">Al je gegenereerde QR codes op één plek</p>
            </div>
            
            <div class="mx-auto w-full max-w-6xl">
                <div class="overflow-hidden rounded-2xl bg-white border border-slate-200 shadow-xl">
                    <div class="overflow-x-auto">
                        <table class="w-full text-left">
                            <thead class="bg-slate-50 text-slate-700 border-b border-slate-200">
                                <tr>
                                    <th class="px-6 py-4 hideColumn font-bold text-xs uppercase tracking-wider">QR Code</th>
                                    <th class="px-6 py-4 font-bold text-xs uppercase tracking-wider">URL / Tekst</th>
                                    <th class="px-6 py-4 font-bold text-xs uppercase tracking-wider">Acties</th>
                                    <th class="px-6 py-4 hideColumn font-bold text-xs uppercase tracking-wider"></th>
                                </tr>
                            </thead>
                            <tbody class="divide-y divide-slate-100">
                                <tr v-for="(item, index) in reversedSavedQRs" :key="index" class="hover:bg-slate-50 transition-colors duration-150">
                                    <td class="px-6 py-4 hideColumn">
                                        <div class="p-2 bg-slate-50 rounded-lg border border-slate-200 inline-block">
                                            <img :src="item.dataUrl" alt="Saved QR Code" class="qrcode-small" />
                                        </div>
                                    </td>
                                    <td class="px-6 py-4 align-middle">
                                        <div class="max-w-md break-words text-slate-700 text-sm leading-relaxed font-medium">
                                            {{ item.url }}
                                        </div>
                                    </td>
                                    <td class="px-6 py-4 align-middle">
                                        <button 
                                            @click="downloadImageFromElement(item)"
                                            class="inline-flex items-center gap-2 bg-indigo-600 hover:bg-indigo-700 text-white rounded-lg px-4 py-2.5 font-semibold shadow-md hover:shadow-lg transition-all duration-200 transform hover:scale-105 active:scale-95 text-sm"
                                        >
                                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M4 16v1a3 3 0 003 3h10a3 3 0 003-3v-1m-4-4l-4 4m0 0l-4-4m4 4V4"></path>
                                            </svg>
                                            Download
                                        </button>
                                    </td>
                                    <td class="px-6 py-4 hideColumn align-middle">
                                        <button 
                                            @click="removeItemFromSavedQRs(item)"
                                            class="inline-flex items-center gap-2 bg-red-500 hover:bg-red-600 text-white rounded-lg px-4 py-2.5 font-semibold shadow-md hover:shadow-lg transition-all duration-200 transform hover:scale-105 active:scale-95 text-sm"
                                        >
                                            <svg class="w-4 h-4" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M19 7l-.867 12.142A2 2 0 0116.138 21H7.862a2 2 0 01-1.995-1.858L5 7m5 4v6m4-6v6m1-10V4a1 1 0 00-1-1h-4a1 1 0 00-1 1v3M4 7h16"></path>
                                            </svg>
                                            Verwijder
                                        </button>
                                    </td>
                                </tr>
                            </tbody>
                        </table>
                    </div>
                </div>
            </div>
        </div>

        <!-- Empty State -->
        <div v-else class="text-center py-20 animate-fade-in">
            <div class="inline-flex items-center justify-center w-20 h-20 rounded-full bg-slate-100 text-slate-400 mb-6 shadow-inner">
                <svg class="w-10 h-10" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M20 13V6a2 2 0 00-2-2H6a2 2 0 00-2 2v7m16 0v5a2 2 0 01-2 2H6a2 2 0 01-2-2v-5m16 0h-2.586a1 1 0 00-.707.293l-2.414 2.414a1 1 0 01-.707.293h-3.172a1 1 0 01-.707-.293l-2.414-2.414A1 1 0 006.586 13H4"></path>
                </svg>
            </div>
            <p class="text-slate-600 text-xl font-semibold mb-2">Nog geen QR codes gegenereerd</p>
            <p class="text-slate-500 text-base">Genereer je eerste QR code hierboven</p>
        </div>
    </div>
</template>

<script>
import QRCode from "qrcode";

export default {
    name: "QRCodeGenerator",
    data() {
        return {
            url: "",
            qrCodeDataUrl: null,
            savedQRs: [],
        };
    },
    created() {
        this.loadSavedQRs();
    },
    computed: {
        reversedSavedQRs() {
            // Return a reversed copy of the saved QRs array
            return [...this.savedQRs].reverse();
        }
    },
    methods: {
        removeItemFromSavedQRs(item) {
            this.savedQRs = this.savedQRs.filter((qr) => qr.url !== item.url);
            localStorage.setItem("qrCodes", JSON.stringify(this.savedQRs));
        },
        async generateQRCode() {

            const options = {
                errorCorrectionLevel: "H",
                type: "image/png",
                quality: 1,
                margin: 1,
                scale: 10,
            };
            try {
                this.qrCodeDataUrl = await QRCode.toDataURL(this.url, options);
                this.saveQR();
            } catch (error) {
                console.error("Failed to generate QR Code:", error);
            }
        },
        downloadImage() {
            const link = document.createElement("a");
            link.href = this.qrCodeDataUrl;
            link.download = "QRCode.png";
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        },
        downloadImageFromElement(el) {
            const link = document.createElement("a");
            link.href = el.dataUrl;
            link.download = el.url + "-qrcode.png";
            document.body.appendChild(link);
            link.click();
            document.body.removeChild(link);
        },
        saveQR() {

            const qrData = { url: this.url, dataUrl: this.qrCodeDataUrl };

            // Save the QR code data to local storage if it doesn't exist
            if (!this.savedQRs.some((item) => item.url === this.url)) {
                this.savedQRs.push(qrData);
                localStorage.setItem("qrCodes", JSON.stringify(this.savedQRs));
            }
        },
        loadSavedQRs() {
            const savedData = localStorage.getItem('qrCodes');
            if (savedData) {
                this.savedQRs = JSON.parse(savedData);
            }
        }
    },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap");

* {
    font-family: "Inter", -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
    box-sizing: border-box;
}

.qr-code-generator {
    text-align: center;
}

.qrcode-large {
    max-width: 350px;
    max-height: 350px;
    width: 100%;
    height: auto;
    border-radius: 16px;
}

.qrcode-small {
    width: 70px;
    height: 70px;
    border-radius: 8px;
}

/* Advanced Animations */
@keyframes fadeInDown {
    from {
        opacity: 0;
        transform: translateY(-30px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes slideUp {
    from {
        opacity: 0;
        transform: translateY(50px);
    }
    to {
        opacity: 1;
        transform: translateY(0);
    }
}

@keyframes fadeIn {
    from {
        opacity: 0;
    }
    to {
        opacity: 1;
    }
}

@keyframes scaleIn {
    from {
        opacity: 0;
        transform: scale(0.9);
    }
    to {
        opacity: 1;
        transform: scale(1);
    }
}

@keyframes shakeHorizontal {
    0%, 100% {
        transform: translateX(0);
    }
    10%, 30%, 50%, 70%, 90% {
        transform: translateX(-8px);
    }
    20%, 40%, 60%, 80% {
        transform: translateX(8px);
    }
}

@keyframes pulseGlow {
    0%, 100% {
        opacity: 0.3;
    }
    50% {
        opacity: 0.5;
    }
}

.animate-fade-in-down {
    animation: fadeInDown 0.8s ease-out;
}

.animate-slide-up {
    animation: slideUp 1s ease-out;
}

.animate-fade-in {
    animation: fadeIn 0.8s ease-out;
}

.animate-scale-in {
    animation: scaleIn 0.6s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.animate-shake-horizontal {
    animation: shakeHorizontal 0.6s ease-in-out;
}

.animate-pulse-slow {
    animation: pulseGlow 3s ease-in-out infinite;
}

/* Responsive Design */
@media only screen and (max-width: 640px) {
    .hideColumn {
        display: none;
    }
    
    .qrcode-large {
        max-width: 280px;
        max-height: 280px;
    }
}

/* Enhanced transitions */
button {
    transition: all 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}

input {
    transition: all 0.3s ease-in-out;
}

/* Glassmorphism effects */
input::placeholder {
    transition: all 0.3s ease;
}

input:focus::placeholder {
    opacity: 0.6;
    transform: translateX(4px);
}

/* Focus states for accessibility */
button:focus-visible,
input:focus-visible {
    outline: 3px solid rgba(255, 255, 255, 0.6);
    outline-offset: 3px;
}

/* Hover glow effects */
button:hover {
    filter: brightness(1.1);
}

/* 3D transform effects */
.group:hover .transform {
    transform-style: preserve-3d;
}

/* Smooth opacity transitions */
* {
    -webkit-tap-highlight-color: transparent;
}

/* Custom selection */
::selection {
    background-color: rgba(255, 255, 255, 0.3);
    color: white;
}
</style>
