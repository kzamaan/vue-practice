<template>
    <div class="card bg-transparent border-0">
        <div v-if="!authUser" class="card-body p-0">
            <h4>লগইন করুন</h4>
            <SocialLogin />
        </div>
        <div v-else class="card-body p-0">
            <h4 class="user__link p-3">
                <span class="d-flex align-items-center px-3">
                    {{ authUser.name }}
                </span>
            </h4>
        </div>
        <div class="card-body p-0 mt-4">
            <h6>সর্বশেষ নিবন্ধিত ব্যবহারকারী</h6>
            <div v-if="users.length > 0">
                <div v-for="(user, index) in users" :key="index" class="p-1 mb-1">
                    <router-link :to="`/profile/${user.username}`" class="text-decoration-none text-dark">
                        <div class="d-flex align-items-center">
                            <img
                                :src="`https://ui-avatars.com/api/?background=random&name=${user.name}`"
                                class="img-circle user_image"
                                alt="Profile Image" />
                            <div class="ms-3">
                                <p class="m-0">{{ user.name }}</p>
                                <p class="m-0">{{ user.user_created_at }}</p>
                            </div>
                        </div>
                    </router-link>
                </div>
            </div>
        </div>
        <div class="card-footer p-0 bg-transparent mt-3">
            <ul>
                <li>Privacy Policy</li>
                <li>Terms & Conditions</li>
                <li>About Us</li>
            </ul>
        </div>
    </div>
</template>

<script>
    import SocialLogin from '@/components/SocialLogin.vue';
    export default {
        name: 'RightSideBar',
        components: {
            SocialLogin,
        },
        computed: {
            users() {
                return this.$store.getters.getUsers;
            },
            authUser() {
                return this.$store.getters.user;
            },
        },
    };
</script>
<style lang="scss" scoped>
    .user__link {
        border-radius: 5px;
        border: 1px solid #fde68a;
        background: #fef3c7;
        position: relative;
        &::after {
            content: '';
            width: 10px;
            height: 10px;
            background: green;
            position: absolute;
            left: 10px;
            border-radius: 50%;
            bottom: 50%;
            margin-bottom: -5px;
        }
    }
    .img-circle {
        border-radius: 50%;
    }
    .user_image {
        width: 60px;
    }
</style>
