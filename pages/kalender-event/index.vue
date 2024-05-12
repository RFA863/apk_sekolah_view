<template>
  <div>
    <div class="font-bold text-4xl mx-12 my-6">Kalender Event</div>
    <div class="bg-[#D8EFE9] rounded-lg p-10 m-5">
      <div class="mb-5">
        <NuxtLink to="/kalender-event/create">
          <Button label="Event Baru" severity="info" />
        </NuxtLink>
      </div>
      <DataTable
        v-model:selection="selectedData"
        :value="dataTable"
        dataKey="id"
        selectionMode="single"
        :metaKeySelection="false"
      >
        <Column
          v-for="col of columns"
          :field="col.field"
          :header="col.header"
        />
        <Column header="Actions">
          <template #body="slotProps">
            <div class="flex gap-4">
              <Button
                label="Edit"
                severity="warning"
                @click="edit(slotProps.data)"
              />
              <Button
                label="Delete"
                severity="danger"
                @click="deleteData(slotProps.data)"
              />
            </div>
          </template>
        </Column>
      </DataTable>
    </div>
    <Toast />
    <ConfirmDialog></ConfirmDialog>
  </div>
</template>

<script setup>
const confirm = useConfirm();
const toast = useToast();

const dataTable = ref([]);
const selectedData = ref(null);

const columns = [
  { field: "no", header: "No" },
  { field: "judul", header: "judul" },
  { field: "tanggal", header: "Tanggal" },
  { field: "deskripsi", header: "Deskripsi" },
  { field: "tempat", header: "Tempat" },
  { field: "penanggungjawab", header: "Penanggung Jawab" },
  { field: "kontak", header: "Kontak" },

  // { field: "action", header: "Action" },
];

const edit = (rowData) => {
  selectedData.value = rowData;
  if (selectedData.value.id !== null) {
    navigateTo("/kalender-event/" + selectedData.value.id);
  }
};

const deleteData = (rowData) => {
  selectedData.value = rowData;
  if (selectedData.value.id !== null) {
    confirm.require({
      message: "Anda Yakin Ingin Menghapus Data ini?",
      header: "Danger Zone",
      // icon: "pi pi-info-circle",
      rejectLabel: "Cancel",
      acceptLabel: "Delete",
      rejectClass: "bg-white text-gray-700 border-slate-700 hover:bg-white  ",
      acceptClass:
        "bg-red-600 border-slate-700 hover:bg-red-700 hover:border-slate-700",
      accept: () => {
        deleteTableData();
      },
      // reject: () => {
      //   toast.add({
      //     severity: "error",
      //     summary: "Rejected",
      //     detail: "You have rejected",
      //     life: 3000,
      //   });
      // },
    });
  }
};

const fetchData = async () => {
  try {
    const response = await fetch(
      "http://127.0.0.1:8000/api/sekolah/kalender_event"
    );
    const listData = await response.json();
    const data = listData.data;
    dataTable.value = data.map((item, i) => ({
      id: item.id,
      no: i + 1,
      judul: item.judul,
      tanggal: item.tanggal,
      deskripsi: item.deskripsi,
      tempat: item.tempat,
      penanggungjawab: item.penanggungjawab,
      kontak: item.kontak,
    }));
  } catch (error) {
    console.error("Error fetching data:", error);
  }
};

const deleteTableData = async () => {
  try {
    const response = await fetch(
      "http://localhost:8000/api/sekolah/kalender_event/" +
        selectedData.value.id,
      {
        method: "DELETE",
        headers: {
          "Content-Type": "application/json",
          // 'Authorization': 'Bearer your_token_here', // Ganti your_token_here dengan token yang valid
        },
      }
    );

    if (response.ok) {
      toast.add({
        severity: "success",
        summary: "Success Message",
        detail: "Data Berhasi dihapus",
        life: 3000,
      });
      fetchData();
    } else {
      toast.add({
        severity: "error",
        summary: "Error Message",
        detail: "Data Gagal dihapus",
        life: 3000,
      });
    }
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
</script>
