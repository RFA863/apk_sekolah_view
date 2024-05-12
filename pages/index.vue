<template>
  <div>
    <div
      class="flex justify-center font-bold text-4xl text-[#252B3B] py-6 h-full"
    >
      APLIKASI E-SEKOLAH
    </div>

    <div class="text-white mx-14 my-6 flex justify-around flex-wrap">
      <NuxtLink to="/absen">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon
            name="material-symbols:contract-edit-outline-rounded"
            color="gray"
            size="32px"
          />
          <p class="flex justify-center w-full">Absen</p>
        </div>
      </NuxtLink>

      <NuxtLink to="/bimbingan-konseling">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon
            name="material-symbols:calendar-month-outline-rounded"
            color="gray"
            size="32px"
          />
          <p class="flex justify-center w-full">Form Konsultasi Guru BK</p>
        </div>
      </NuxtLink>

      <NuxtLink to="/coming-soon">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon
            name="material-symbols:stacks-outline-rounded"
            color="gray"
            size="32px"
          />
          <p class="flex justify-center w-full">Form Referensi Buku</p>
        </div>
      </NuxtLink>

      <NuxtLink to="/coming-soon">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon
            name="material-symbols:book-4-outline-rounded"
            color="gray"
            size="32px"
          />
          <p class="flex justify-center w-full">Mata Pelajaran</p>
        </div>
      </NuxtLink>

      <NuxtLink to="/kalender-event">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon
            name="material-symbols:event-available-outline"
            color="gray"
            size="32px"
          />
          <p class="flex justify-center w-full">Kalender of Event</p>
        </div>
      </NuxtLink>

      <NuxtLink to="/tugas">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon
            name="material-symbols:edit-outline-rounded"
            color="gray"
            size="32px"
          />
          <p class="flex justify-center w-full">Tugas Sekolah</p>
        </div>
      </NuxtLink>

      <NuxtLink to="/catatan">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon name="fluent:note-24-regular" color="gray" size="32px" />
          <p class="flex justify-center w-full">Catatan</p>
        </div>
      </NuxtLink>

      <NuxtLink to="coming-soon">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon name="vaadin:money" color="gray" size="32px" />
          <p class="flex justify-center w-full">Tabungan</p>
        </div>
      </NuxtLink>

      <NuxtLink to="coming-soon">
        <div
          class="flex items-center gap-2 w-72 px-6 py-4 bg-[#252B3B] rounded-lg my-8 transition-colors duration-300 hover:bg-slate-700 hover:text-gray-300"
        >
          <Icon name="mingcute:group-3-line" color="gray" size="32px" />
          <p class="flex justify-center w-full">Form Diskusi</p>
        </div>
      </NuxtLink>
    </div>
  </div>
</template>
