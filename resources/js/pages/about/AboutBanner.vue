<template>
    <div class="relative w-full h-fit py-12 px-6 md:px-16"
        :style="{ backgroundImage: `url(${heroImage})`, backgroundSize: 'cover', backgroundPosition: 'center' }">
        <!-- Title -->
<<<<<<< HEAD
        <h2 class="text-white text-3xl sm:text-4xl md:text-5xl font-bold font-montserrat mb-6 text-left">
=======
        <h2 class="text-white text-3xl sm:text-4xl md:text-5xl font-bold font-cormorant mb-6 text-left">
>>>>>>> 45bc8954c5b95a95d1ab5a78f624a5d74aa6fd4a
            Our partners
        </h2>
        <!-- Partner Logos -->
        <div class="flex flex-col items-center space-y-6">
            <div class="flex flex-wrap justify-center items-center gap-20">
                <img src="../../images/logos5.png" alt="Ascott Limited" class="w-64 h-85 object-contain">
                <img src="../../images/logo.png" alt="MPDC" class="w-64 h-32 object-contain">
            </div>
        </div>


        <!-- Two-Column Content (Tightly Packed) -->
        <div class="grid grid-cols-1 md:grid-cols-2 mt-6">
            <!-- Left: Text Section (No Gap) -->
<<<<<<< HEAD
            <div class="bg-[#1E3A5F] bg-opacity-40 text-white p-4 md:p-6 flex items-center">
=======
            <div class="bg-[#1E3A5F] text-white p-4 md:p-6 flex items-center">
>>>>>>> 45bc8954c5b95a95d1ab5a78f624a5d74aa6fd4a
                <p class="text-xl md:text-xl leading-tight">
                    Malveda Properties and Development Corporation has established strategic partnership with leading
                    global hotel operators.

                    Our collaboration with The Ascott Limited, a highly respected name in real estate and hospital
                    industry, underscores our steadfast commitment to delivering exceptional service standard and
                    providing incomparable experiences for our clients.

                    This collaboration reflects our dedication to excellence and positions us as a key player in
                    providing premium property investment.
                </p>
            </div>

            <!-- Right: Image Section (No Gap) -->
            <div class="w-full">
                <img src="../../images/mate1.jpg" class="w-full object-cover h-full">
            </div>
        </div>
    </div>
</template>

<script setup lang="ts">
import heroImage from '../../images/bgwave.jpg';
</script>

<style scoped>
/* Import Custom Font */
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@400;700&display=swap');

<<<<<<< HEAD
.font-montserrat {
  font-family: 'Montserrat', sans-serif;
=======
.font-cormorant {
    font-family: 'Cormorant Garamond', serif;
>>>>>>> 45bc8954c5b95a95d1ab5a78f624a5d74aa6fd4a
}
</style>
