<template>
  <div>
    <!-- Button trigger modal -->
    <button
      type="button"
      class="btn"
      @click="openEditModal(user.userID)"
      data-bs-toggle="modal"
      :data-bs-target="'#texampleModal' + user.userID"
    >
      Edit
    </button>

    <!-- Modal -->
    <div
      class="modal fade p-3"
      :id="'texampleModal' + user.userID"
      tabindex="-1"
      :aria-labelledby="'texampleModalLabel' + user.userID"
      aria-hidden="true"
    >
      <div class="modal-dialog">
        <div class="modal-content">
          <div class="modal-header">
            <h1 class="modal-title fs-5" id="texampleModalLabel3">
              Update User:
            </h1>
            <button
              type="button"
              class="btn-close"
              data-bs-dismiss="modal"
              aria-label="Close"
            ></button>
          </div>
          <div class="modal-body card">
            <div class="mb-3 text-font">
              <label for="">UserID</label> <br>
              <input
                type="text"
                placeholder="ID"
                v-model="editingUser.userID"
              />
            </div>
            <div class="mb-3 text-font">
              <label for="">First Name</label> <br>
            <input
              type="text"
              placeholder="first name"
              v-model="editingUser.firstName"
            />
            </div>
            <div class="mb-3 text-font">
              <label for="">Last Name</label> <br>
            <input
              type="text"
              placeholder="last name"
              v-model="editingUser.lastName"
            />
            </div>
            <div class="mb-3 text-font">
              <label for="">Age</label> <br>
            <input
              type="number"
              placeholder="age"
              v-model="editingUser.userAge"
            />
            </div>
            <div class="mb-3 text-font">
              <label for="">Gender</label> <br>
            <input
              type="text"
              placeholder="gender"
              v-model="editingUser.gender"
            />
            </div>
            <div class="mb-3 text-font">
              <label for="">Role</label> <br>
            <input
              type="text"
              placeholder="role"
              v-model="editingUser.userRole"
            />
            </div>
            <div class="mb-3 text-font">
              <label for="">Email Address</label> <br>
            <input
              type="text"
              placeholder="email address"
              v-model="editingUser.emailAdd"
            />
            </div>
            <div class="mb-3 text-font">
              <label for="">Profile Image</label> <br>
            <input
              type="text"
              placeholder="profile image"
              v-model="editingUser.userProfile"
            />
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn" data-bs-dismiss="modal">
              Close
            </button>
            <button
              type="button"
              class="btn"
              @click="updateProduct(user.userID)"
            >
              Update!
            </button>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["user"],
  data() {
    return {
      editingUser: {
        ...this.user,
      },
      editingUserID: null,
      model: {
        user: {
          firstName: "",
          lastName: "",
          userAge: "",
          gender: "",
          userRole: "",
          emailAdd: "",
          userProfile: "",
        },
      },
    };
  },
  computed: {
    currentUser() {
      return this.$store.state.user;
    },
  },
  methods: {
    openEditModal(id) {
      console.log("reached");
      this.editingUserID = id;
      this.editingUser = {
        ...this.$store.state.users.find((user) => user.userID === id),
      };
    },
    updateProduct(id) {
      this.$store
        .dispatch("updateUser", {
          userID: id,
          data: { ...this.editingUser },
        })
        .then(() => {
          console.log("User updated!");
          setTimeout(() => {
            window.location.reload();
          }, 5000);
        })
        .catch((err) => {
          console.error("Error updating: ", err);
        });
    },
  },
};
</script>

<style scoped>


.btn {
  border: 3px solid #ee4823;
  border-radius: 20px;
  background: #faf9e8;
}

.btn:hover {
  border: 3px solid #faf9e8;
  background: #ee4823;
  color: #faf9e8;
}

.card{
  background: #45A245;
}

input{
  border-radius: 10px;
  width: 100%;
  padding: 2px;
}
</style>
