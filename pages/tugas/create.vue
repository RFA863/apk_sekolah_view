<template>
  <div>
    <div class="font-bold text-4xl mx-12 my-6">Input Tugas</div>
    <div class="bg-[#D8EFE9] rounded-lg p-10 m-5">
      <form @submit.prevent="handleSubmit">
        <table class="w-full border-separate border-spacing-2">
          <tr>
            <td>Nama</td>
            <td>:</td>
            <td>
              <Dropdown
                v-model="selectedNama"
                :options="nama"
                showClear
                optionLabel="name"
                placeholder="Nama Siswa"
                class="w-1/2"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Guru</td>
            <td>:</td>
            <td>
              <Dropdown
                v-model="selectedGuru"
                :options="guru"
                showClear
                optionLabel="name"
                placeholder="Guru Pemberi Tugas"
                class="w-1/2"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Mata Pelajaran</td>
            <td>:</td>
            <td>
              <Dropdown
                v-model="selectedMatpel"
                :options="matpel"
                showClear
                optionLabel="name"
                placeholder="Mata Pelajaran"
                class="w-1/2"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Tanggal Tugas</td>
            <td>:</td>
            <td>
              <Calendar
                v-model="tgl"
                showButtonBar
                showIcon
                class="w-1/2"
                placeholder="Tanggal Tugas"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Tanggal Pengumpulan</td>
            <td>:</td>
            <td>
              <Calendar
                v-model="tgl_pengumpulan"
                showButtonBar
                showIcon
                class="w-1/2"
                placeholder="Tanggal Pengumpulan"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Deskripsi Tugas</td>
            <td>:</td>
            <td colspan="3">
              <InputText
                type="text"
                v-model="deskripsi"
                class="w-full"
                placeholder="Deskripsi Tugas"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Isi Tugas</td>
            <td>:</td>
            <td>
              <InputText
                type="text"
                v-model="isi_tugas"
                class="w-full"
                placeholder="Isi Tugas"
                required
              />
            </td>
          </tr>
        </table>

        <div class="flex justify-end gap-4 my-5">
          <NuxtLink to="/tugas">
            <Button label="Back" />
          </NuxtLink>
          <Button label="Submit" type="submit" />
        </div>
      </form>
    </div>
    <Toast />
  </div>
</template>

<script setup>
import { ref, onMounted } from "vue";

const toast = useToast();

const tgl = ref();
const tgl_pengumpulan = ref();
const deskripsi = ref();
const isi_tugas = ref();

const selectedNama = ref();
const selectedGuru = ref();
const selectedMatpel = ref();

const nama = ref([]);
const guru = ref([]);
const matpel = ref([]);

const fetchSiswa = async () => {
  try {
    const response = await fetch("http://127.0.0.1:8000/api/sekolah/siswa");
    const listData = await response.json();
    const data = listData.data;
    nama.value = data.map((item) => ({
      name: item.nama,
      code: item.id,
    }));
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

const fetchGuru = async () => {
  try {
    const response = await fetch("http://127.0.0.1:8000/api/sekolah/guru");
    const listData = await response.json();
    const data = listData.data;
    guru.value = data.map((item) => ({
      name: item.nama,
      code: item.id,
    }));
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

const fetchMatpel = async () => {
  try {
    const response = await fetch("http://127.0.0.1:8000/api/sekolah/matpel");
    const listData = await response.json();
    const data = listData.data;
    matpel.value = data.map((item) => ({
      name: item.pelajaran,
      code: item.id,
    }));
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

onMounted(() => {
  fetchSiswa();
  fetchGuru();
  fetchMatpel();
});

const handleSubmit = async () => {
  const date = new Date(tgl.value);
  const deadline = new Date(tgl_pengumpulan.value);

  const data = {
    siswa_id: selectedNama.value.code,
    guru_id: selectedGuru.value.code,
    matpel_id: selectedMatpel.value.code,
    tgl: date.toISOString().split("T")[0],
    tgl_pengumpulan: deadline.toISOString().split("T")[0],
    deskripsi: deskripsi.value,
    isi_tugas: isi_tugas.value,
  };

  try {
    const response = await fetch(
      "http://localhost:8000/api/sekolah/tugas_sekolah",
      {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          // 'Authorization': 'Bearer your_token_here', // Ganti your_token_here dengan token yang valid
        },
        body: JSON.stringify(data),
      }
    );

    if (response.ok) {
      toast.add({
        severity: "success",
        summary: "Success Message",
        detail: "Input Data Berhasi",
        life: 3000,
      });
      navigateTo("/tugas");
    } else {
      toast.add({
        severity: "error",
        summary: "Error Message",
        detail: "Input Data Gagal",
        life: 3000,
      });
    }
  } catch (error) {
    console.error("Terjadi kesalahan:", error);
  }
};
</script>
