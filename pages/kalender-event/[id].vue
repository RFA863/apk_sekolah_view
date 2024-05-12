<template>
  <div>
    <div class="font-bold text-4xl mx-12 my-6">Update Event</div>
    <div class="bg-[#D8EFE9] rounded-lg p-10 m-5">
      <form @submit.prevent="handleSubmit">
        <table class="w-full border-separate border-spacing-2">
          <tr>
            <td>Judul</td>
            <td>:</td>
            <td>
              <InputText
                type="text"
                v-model="judul"
                class="w-1/2"
                placeholder="judul"
                required
              />
            </td>
          </tr>

          <tr>
            <td>Penanggung Jawab</td>
            <td>:</td>
            <td colspan="3">
              <InputText
                type="text"
                v-model="penanggungjawab"
                class="w-1/2"
                placeholder="Penanggung Jawab"
                required
              />
            </td>
          </tr>
          <tr>
            <td>Kontak</td>
            <td>:</td>
            <td>
              <InputText
                type="text"
                v-model="kontak"
                class="w-1/2"
                placeholder="Kontak"
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

          <tr>
            <td>Deskripsi</td>
            <td>:</td>
            <td colspan="3">
              <InputText
                type="text"
                v-model="deskripsi"
                class="w-1/2"
                placeholder="Deskripsi"
                required
              />
            </td>
          </tr>
        </table>

        <div class="flex justify-end gap-4 my-5">
          <NuxtLink to="/kalender-event">
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

const route = useRoute();
const toast = useToast();

const judul = ref();
const tanggal = ref();
const tempat = ref();
const penanggungjawab = ref();
const kontak = ref();
const deskripsi = ref();

const fetchData = async () => {
  try {
    const response = await fetch(
      "http://127.0.0.1:8000/api/sekolah/kalender_event/" + route.params.id
    );
    const listData = await response.json();
    const data = listData.data;

    judul.value = data.judul;
    tanggal.value = data.tanggal;
    deskripsi.value = data.deskripsi;
    penanggungjawab.value = data.penanggungjawab;
    kontak.value = data.kontak;
    tempat.value = data.tempat;
  } catch (error) {
    toast.add({
      severity: "error",
      summary: "Error Message",
      detail: error,
      life: 3000,
    });
  }
};

onMounted(() => {
  fetchData();
});

const handleSubmit = async () => {
  const date = new Date(tanggal.value);

  const data = {
    judul: judul.value,
    tanggal: date.toISOString().split("T")[0],
    deskripsi: deskripsi.value,
    tempat: tempat.value,
    penanggungjawab: penanggungjawab.value,
    kontak: kontak.value,
  };

  try {
    const response = await fetch(
      "http://localhost:8000/api/sekolah/kalender_event/" + route.params.id,
      {
        method: "PUT",
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
      navigateTo("/kalender-event");
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
