<template>
    <footer id="okc_footer" class="bg-[#1a1a1a] p-10 md:p-14 lg:p-16 text-white">
        <div class="footer_inner flex flex-wrap flex-col md:flex-row justify-center gap-[3.6rem]">
            <div class="footer_group text-center">
                <NuxtLink to="/signup">
                    <el-button class="font-medium nm w-full md:w-56" type="primary">
                        JOIN OKCUPID
                    </el-button>
                </NuxtLink>

                <p class="mt-4 leading-7 text-sm">© OkCupid {{ new Date().getFullYear() }}</p>
            </div>

            <div class="footer_group">
                <h2 class="font-semibold mb-4">Language</h2>

                <el-button 
                    class="border border-white bg-transparent text-white w-32 flex flex-row-reverse justify-between" 
                    plain 
                    icon="el-icon-arrow-right">
                    English
                </el-button>
            </div>

            <div class="footer_group " v-for="(item, index) in footerNavigationData" :key="index">
                <h2 class="font-semibold">{{ item.title }}</h2>
                <ul>
                    <li v-for="(subItem, index2) in item.children" :key="index2">
                        <a :href="subItem.link">{{ subItem.title }}</a>
                    </li>
                </ul>
            </div>
        </div>
    </footer>
</template>

<script>
    export default {
        name: 'FooterNavigation',
        data() {
            return {
                footerNavigationData: [
                    {
                        title: 'Company',
                        children: [
                            {
                                title: 'About',
                                link: 'https://www.okcupid.com/about',
                            },
                            {
                                title: 'Careers',
                                link: 'https://www.okcupid.com/careers',
                            },
                            {
                                title: 'Press',
                                link: 'https://www.okcupid.com/press',
                            },
                            {
                                title: 'Ad Choices',
                                link: 'https://www.okcupid.com/legal/privacy#third-parties',
                            },
                        ],
                    },
                    {
                        title: 'Conditions',
                        children: [
                            {
                                title: 'Privacy',
                                link: 'https://www.okcupid.com/legal/privacy',
                            },
                            {
                                title: 'Cookies – Manage preferences',
                                link: 'https://www.okcupid.com/legal/cookies',
                            },
                            {
                                title: 'Terms',
                                link: 'https://www.okcupid.com/legal/terms',
                            },
                            {
                                title: 'Community Guidelines',
                                link: 'https://help.okcupid.com/article/142-community-guidelines',
                            },
                        ],
                    },
                    {
                        title: 'Contact',
                        children: [
                            {
                                title: 'Support',
                                link: 'https://help.okcupid.com/',
                            },
                            {
                                title: 'Security',
                                link: 'https://www.okcupid.com/security',
                            },
                            {
                                title: 'Safety Tips',
                                link: 'https://www.okcupid.com/legal/safety-tips',
                            },
                            {
                                title: 'Impressum',
                                link: 'https://www.okcupid.com/legal/privacy#how-to-contact-us',
                            },
                        ],
                    },
                    {
                        title: 'Follow',
                        children: [
                            {
                                title: 'Blog',
                                link: 'https://theblog.okcupid.com/',
                            },
                            {
                                title: 'Tech Blog',
                                link: 'https://tech.okcupid.com/',
                            },
                            {
                                title: 'Facebook',
                                link: 'https://facebook.com/okcupid',
                            },
                            {
                                title: 'Instagram',
                                link: 'https://instagram.com/okcupid',
                            },
                            {
                                title: 'Twitter',
                                link: 'https://twitter.com/okcupid',
                            },
                        ],
                    },
                    {
                        title: 'Special',
                        children: [
                            {
                                title: 'Redeem Promotion',
                                link: '#',
                            },
                            {
                                title: 'Download Apps',
                                link: 'https://www.okcupid.com/downloads',
                            },
                        ],
                    },
                ],
            }
        },
    }
</script>

