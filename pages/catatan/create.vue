<template>
  <div>
    <div class="font-bold text-4xl mx-12 my-6">Input Catatan</div>
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
            <td>Judul</td>
            <td>:</td>
            <td colspan="3">
              <InputText
                type="text"
                v-model="judul"
                class="w-1/2"
                placeholder="Judul"
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
            <td>Isi</td>
            <td>:</td>
            <td>
              <InputText
                type="text"
                v-model="isi"
                class="w-full"
                placeholder="Isi"
                required
              />
            </td>
          </tr>
        </table>

        <div class="flex justify-end gap-4 my-5">
          <NuxtLink to="/catatan">
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

const judul = ref();
const tanggal = ref();
const isi = ref();

const selectedNama = ref();

const nama = ref([]);

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

onMounted(() => {
  fetchSiswa();
});

const handleSubmit = async () => {
  const date = new Date(tanggal.value);

  const data = {
    siswa_id: selectedNama.value.code,

    judul: judul.value,
    tanggal: date.toISOString().split("T")[0],
    isi: isi.value,
  };

  try {
    const response = await fetch("http://localhost:8000/api/sekolah/note", {
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
        detail: "Input Data Berhasi",
        life: 3000,
      });
      navigateTo("/catatan");
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
