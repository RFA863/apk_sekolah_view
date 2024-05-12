<template>
  <div class="bg-[#252B3B] text-white">
    <NuxtLink to="/">
      <p class="flex justify-center items-center text-3xl font-bold py-8">
        SEKOLAH
      </p>
    </NuxtLink>
    <ul>
      <NuxtLink to="/absen">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon
            name="material-symbols:contract-edit-outline-rounded"
            color="gray"
            size="32px"
          />
          <p>Absen</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/bimbingan-konseling">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon
            name="material-symbols:calendar-month-outline-rounded"
            color="gray"
            size="32px"
          />
          <p>Form Konsultasi Guru BK</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/coming-soon">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon
            name="material-symbols:stacks-outline-rounded"
            color="gray"
            size="32px"
          />
          <p>Form Referensi Buku</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/coming-soon">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon
            name="material-symbols:book-4-outline-rounded"
            color="gray"
            size="32px"
          />
          <p>Mata Pelajaran</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/kalender-event">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon
            name="material-symbols:event-available-outline"
            color="gray"
            size="32px"
          />
          <p>Kalender of Event</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/tugas">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon
            name="material-symbols:edit-outline-rounded"
            color="gray"
            size="32px"
          />
          <p>Tugas Sekolah</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/catatan">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon name="fluent:note-24-regular" color="gray" size="32px" />
          <p>Catatan</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/coming-soon">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon name="vaadin:money" color="gray" size="32px" />
          <p>Tabungan</p>
        </li>
      </NuxtLink>

      <NuxtLink to="/coming-soon">
        <li
          class="py-3 px-14 flex gap-2 item-center transition-colors duration-300 hover:bg-slate-400 hover:text-gray-700"
        >
          <Icon name="mingcute:group-3-line" color="gray" size="32px" />
          <p>Form Diskusi</p>
        </li>
      </NuxtLink>
    </ul>
  </div>
</template>

<script setup></script>
