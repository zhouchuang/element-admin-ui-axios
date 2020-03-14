<template>
  <div class="app-container">
    <el-button type="primary" @click="handleAddRole">New Role</el-button>

    <el-table :data="rolesList" style="width: 100%;margin-top:30px;" border>
      <el-table-column align="center" label="Role Key" width="220">
        <template slot-scope="scope">
          {{ scope.row.key }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="Role Name" width="220">
        <template slot-scope="scope">
          {{ scope.row.name }}
        </template>
      </el-table-column>
      <el-table-column align="header-center" label="Description">
        <template slot-scope="scope">
          {{ scope.row.description }}
        </template>
      </el-table-column>
      <el-table-column align="center" label="Operations">
        <template slot-scope="scope">
          <el-button type="primary" size="small" @click="handleEdit(scope)">Edit</el-button>
          <el-button type="danger" size="small" @click="handleDelete(scope)">Delete</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
import { getRoles } from '@/api/role'
import Axiox from '@/utils/axios'

const defaultRole = {
  key: '',
  name: '',
  description: '',
  routes: []
}
export default {
  data() {
    return {
      role: Object.assign({}, defaultRole),
      rolesList: []
    }
  },
  created() {
    this.getRoles()
    Axiox.get('/ins/app/uploadlist')
      .then(function(response) {
        console.log(response)
      })
      .catch(function(error) {
        console.log(error)
      })
  },
  methods: {
    async getRoles() {
      const res = await getRoles()
      this.rolesList = res.data
    }
  }
}
</script>

<style lang="scss" scoped>
  .app-container {
    .roles-table {
      margin-top: 30px;
    }
    .permission-tree {
      margin-bottom: 30px;
    }
  }
</style>
