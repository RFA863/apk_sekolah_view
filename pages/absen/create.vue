<template>
  <div>
    <div class="font-bold text-4xl mx-12 my-6">Absen</div>
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
            <td>Kelas</td>
            <td>:</td>
            <td>
              <Dropdown
                v-model="selectedKelas"
                :options="kelas"
                showClear
                optionLabel="name"
                placeholder="Kelas Siswa"
                class="w-1/2"
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
            <td>Kehadiran</td>
            <td>:</td>
            <td>
              <Dropdown
                v-model="selectedAbsen"
                :options="absen"
                showClear
                optionLabel="name"
                placeholder="Absensi"
                class="w-1/2"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Keterangan</td>
            <td>:</td>
            <td colspan="3">
              <InputText type="text" v-model="keterangan" class="w-full" />
            </td>
          </tr>
        </table>

        <div class="flex justify-end gap-4 my-5">
          <NuxtLink to="/absen">
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

const tanggal = ref();
const keterangan = ref();

const selectedNama = ref();
const selectedAbsen = ref();
const selectedKelas = ref();

const nama = ref([]);
const kelas = ref([]);

const absen = ref([
  { name: "Hadir", code: "Hadir" },
  { name: "Sakit", code: "Sakit" },
  { name: "Izin", code: "Izin" },
  { name: "Alpha", code: "Alpha" },
]);

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

const fetchKelas = async () => {
  try {
    const response = await fetch("http://127.0.0.1:8000/api/sekolah/kelas");
    const listData = await response.json();
    const data = listData.data;
    kelas.value = data.map((item) => ({
      name: item.kelas,
      code: item.id,
    }));
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};
onMounted(() => {
  fetchSiswa();
  fetchKelas();
});

const handleSubmit = async () => {
  const date = new Date(tanggal.value);
  const data = {
    siswa_id: selectedNama.value.code,
    kelas_id: selectedKelas.value.code,
    tanggal: date.toISOString().split("T")[0],
    absensi: selectedAbsen.value.code,
    keterangan: keterangan.value,
  };

  try {
    const response = await fetch("http://localhost:8000/api/sekolah/absen", {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        // 'Authorization': 'Bearer your_token_here', // Ganti your_token_here dengan token yang valid
      },
      body: JSON.stringify(data),
    });

    if (response.ok) {
      toast.add({
        severity: "success",
        summary: "Success Message",
        detail: "Absensi Berhasi",
        life: 3000,
      });
      navigateTo("/absen");
    } else {
      toast.add({
        severity: "error",
        summary: "Error Message",
        detail: "Absensi Gagal",
        life: 3000,
      });
    }
  } catch (error) {
    console.error("Terjadi kesalahan:", error);
  }
};
</script>
