<template>
  <div>
    <div class="font-bold text-4xl mx-12 my-6">Input Konsultasi</div>
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
                placeholder="Guru Bimbingan Konseling"
                class="w-1/2"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Tujuan</td>
            <td>:</td>
            <td colspan="3">
              <InputText
                type="text"
                v-model="tujuan"
                class="w-1/2"
                placeholder="tujuan"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Tanggal</td>
            <td>:</td>
            <td>
              <Calendar
                v-model="tanggal"
                showButtonBar
                showIcon
                class="w-1/2"
                placeholder="Tanggal"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Status</td>
            <td>:</td>
            <td>
              <InputText
                type="text"
                v-model="status"
                class="w-1/2"
                placeholder="Status"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Jam</td>
            <td>:</td>
            <td>
              <Calendar
                v-model="jam"
                timeOnly
                class="w-1/2"
                placeholder="jam"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Tempat</td>
            <td>:</td>
            <td colspan="3">
              <InputText
                type="text"
                v-model="tempat"
                class="w-1/2"
                placeholder="Tempat"
                required
              />
            </td>
          </tr>
        </table>

        <div class="flex justify-end gap-4 my-5">
          <NuxtLink to="/bimbingan-konseling">
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

const tujuan = ref();
const tanggal = ref();
const tempat = ref();
const jam = ref();
const status = ref();

const selectedNama = ref();
const selectedGuru = ref();

const nama = ref([]);
const guru = ref([]);

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
onMounted(() => {
  fetchSiswa();
  fetchGuru();
});

const handleSubmit = async () => {
  const date = new Date(tanggal.value);
  const time = new Date(jam.value);
  const data = {
    siswa_id: selectedNama.value.code,
    guru_id: selectedGuru.value.code,
    tujuan: tujuan.value,
    tanggal: date.toISOString().split("T")[0],
    status: status.value,
    jam: time
      .toLocaleString("id-ID", {
        timeZone: "Asia/Jakarta",
        timeStyle: "medium",
      })
      .replace(/\./g, ":"),
    tempat: tempat.value,
  };

  try {
    const response = await fetch(
      "http://localhost:8000/api/sekolah/konsultasi_bk",
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
      navigateTo("/bimbingan-konseling");
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
