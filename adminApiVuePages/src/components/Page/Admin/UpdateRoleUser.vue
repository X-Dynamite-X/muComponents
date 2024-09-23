<script setup>
import { ref , onMounted } from 'vue';
import { useAdminStore } from "../../../stores/admin";
import { useRoleStore } from '../../../stores/roles'
const adminStore = useAdminStore();
const roleStore = useRoleStore()

// بيانات المستخدمين الوهمية (تحتاج إلى استبدالها ببيانات حقيقية من API)
const users = adminStore.users;

// قائمة الأدوار المتاحة
const roles = roleStore.roles

// حالية النافذة المنبثقة
const isModalOpen = ref(false);
const selectedUser = ref(null);
const selectedRole = ref(null);

// فتح النافذة المنبثقة وتعيين المستخدم المختار
const openRoleModal = (user) => {
  selectedUser.value = user;
  selectedRole.value = user.roles[0].name; // تعيين الدور الحالي للمستخدم
  isModalOpen.value = true;
};

// غلق النافذة المنبثقة
const closeRoleModal = () => {
  isModalOpen.value = false;
  selectedUser.value = null;
  selectedRole.value = null;
};

// تحديث دور المستخدم
const updateUserRole = async () => {
  try {
    // استدعاء API لتحديث دور المستخدم
    await adminStore.updateUser({
      id: selectedUser.value.id,
      role: selectedRole.value,  // تحديث الدور في back-end
    });

    // تحديث الدور محليًا بعد نجاح العملية
    selectedUser.value.roles[0].name = selectedRole.value;

    // غلق النافذة المنبثقة
    closeRoleModal();

    // رسالة نجاح
    alert('User role updated successfully');
  } catch (error) {
    // التعامل مع الأخطاء
    console.error('Error updating user role:', error);
    alert('An error occurred while updating the user role');
  }
};
onMounted(async () => {

  await adminStore.getAllUsers();
  await roleStore.getAllRoles();


});
</script>
<template>
    <div class="max-w-4xl mx-auto p-8 bg-white rounded-lg shadow-lg mt-10">
      <h2 class="text-2xl font-semibold text-gray-900 mb-6">Change User Roles</h2>

      <!-- Table to display users and roles -->
      <table class="min-w-full bg-white">
        <thead>
          <tr>
            <th class="py-2 px-4 text-left">User Name</th>
            <th class="py-2 px-4 text-left">Current Role</th>
            <th class="py-2 px-4 text-center">Action</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="user in users" :key="user.id" class="border-t">
            <td class="py-2 px-4">{{ user.name }}</td>
            <td class="py-2 px-4">{{ user.roles[0].name }}</td>
            <td class="py-2 px-4 text-center">
              <button
                class="bg-blue-500 text-white px-4 py-2 rounded hover:bg-blue-700"
                @click="openRoleModal(user)"
              >
                Change Role
              </button>
            </td>
          </tr>
        </tbody>
      </table>

      <!-- Modal for selecting a new role -->
      <div v-if="isModalOpen" class="fixed inset-0 bg-gray-800 bg-opacity-75 flex items-center justify-center z-50">
  <div class="bg-white p-6 rounded-lg shadow-lg w-full max-w-lg mx-4">
    <h3 class="text-lg font-semibold mb-4">Change Role for {{ selectedUser.name }}</h3>
    <label for="role" class="block text-gray-700 mb-2">Select New Role</label>
    <select v-model="selectedRole" class="w-full px-4 py-2 border rounded-lg focus:outline-none focus:ring-2 focus:ring-blue-500">
      <option v-for="role in roles" :key="role.id" :value="role.name"  >{{ role.name }}</option>
    </select>
    <div class="flex justify-end mt-4">
      <button class="bg-green-500 text-white px-4 py-2 rounded mr-2 hover:bg-green-700" @click="updateUserRole">
        Save
      </button>
      <button class="bg-gray-500 text-white px-4 py-2 rounded hover:bg-gray-700" @click="closeRoleModal">
        Cancel
      </button>
    </div>
  </div>
</div>
    </div>
  </template>
