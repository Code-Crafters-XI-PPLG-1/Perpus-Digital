<template>
  <h2 class="text-center">Riwayat pengunjung</h2>
  <br />
  <nuxt-link to="/tambah">isi buku tamu</nuxt-link>
  <div>
    <table class="table">
      <thead class="table-primary">
        <tr>
          <th>#</th>
          <th>tgl dan waktu</th>
          <th>nama</th>
          <th>anggota</th>
          <th>kelas</th>
          <th>keperluan</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="pengunjung in visitors" :key="pengunjung.id">
          <td>{{ pengunjung.id }}</td>
          <td>{{ pengunjung.tanggal }} {{ pengunjung.waktu }}</td>
          <td>{{ pengunjung.nama }}</td>
          <td>{{ pengunjung.anggota.nama }}</td>
          <td>
            <span v-if="pengunjung.kelas">{{ pengunjung.kelas }}</span>
            <span v-else>-</span>
          </td>
          <td>{{ pengunjung.keperluan }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
const client = useSupabaseClient();
const visitors = ref([]);

async function getData() {
  const { data, error } = await client.from("pengunjung").select(`id, tanggal, waktu, nama, anggota(nama), kelas, keperluan`);
  if (data) visitors.value = data;
}

onMounted(() => getData());
</script>
