<script lang="ts">
    import { Card } from "$lib/components/ui/card";
    import { Switch } from "$lib/components/ui/switch";
    import { browser } from "$app/environment";
    import { onMount } from "svelte";
  
    let isDarkMode = false;
  
    // Social media stats data
    const socialCards = [
      {
        platform: "facebook",
        username: "@nathanf",
        followers: "1987",
        followersLabel: "FOLLOWERS",
        change: { value: 12, type: "up" },
        color: "bg-blue-500",
        icon: { src: '../src/assets/facebook.svg', alt: 'Facebook' }
      },
      {
        platform: "twitter",
        username: "@nathanf",
        followers: "1044",
        followersLabel: "FOLLOWERS",
        change: { value: 99, type: "up" },
        color: "bg-blue-400",
        icon: { src: '../src/assets/twitter.svg', alt: 'Twitter' }
      },
      {
        platform: "instagram",
        username: "@realnathanf",
        followers: "11k",
        followersLabel: "FOLLOWERS",
        change: { value: 1099, type: "up" },
        color: "bg-gradient-to-r from-yellow-400 via-pink-500 to-pink-600",
        icon: { src: '../src/assets/instagram.svg', alt: 'Instagram' }
      },
      {
        platform: "youtube",
        username: "Nathan F.",
        followers: "8239",
        followersLabel: "SUBSCRIBERS",
        change: { value: 144, type: "down" },
        color: "bg-red-600",
        icon: { src: '../src/assets/youtube.svg', alt: 'YouTube' }
      }
    ];
  
    const overviewCards = [
      { title: "Page Views", platform: "facebook", value: "87", change: { value: 3, type: "up" }, icon: { src: '../src/assets/facebook.svg', alt: 'Facebook' } },
      { title: "Likes", platform: "facebook", value: "52", change: { value: 2, type: "down" }, icon: { src: '../src/assets/facebook.svg', alt: 'Facebook' } },
      { title: "Likes", platform: "instagram", value: "5462", change: { value: 2257, type: "up" }, icon: { src: '../src/assets/instagram.svg', alt: 'Instagram' } },
      { title: "Profile Views", platform: "instagram", value: "52k", change: { value: 1375, type: "up" }, icon: { src: '../src/assets/instagram.svg', alt: 'Instagram' } },
      { title: "Retweets", platform: "twitter", value: "117", change: { value: 303, type: "up" }, icon: { src: '../src/assets/twitter.svg', alt: 'Twitter' } },
      { title: "Likes", platform: "twitter", value: "507", change: { value: 553, type: "up" }, icon: { src: '../src/assets/twitter.svg', alt: 'Twitter' } },
      { title: "Likes", platform: "youtube", value: "107", change: { value: 19, type: "down" }, icon: { src: '../src/assets/youtube.svg', alt: 'YouTube' } },
      { title: "Total Views", platform: "youtube", value: "1407", change: { value: 12, type: "down" }, icon: { src: '../src/assets/youtube.svg', alt: 'YouTube' } }
    ];
  
    function toggleDarkMode() {
      isDarkMode = !isDarkMode;
      if (browser) {
        document.documentElement.classList.toggle('dark');
      }
    }
  
    onMount(() => {
      if (browser) {
        isDarkMode = document.documentElement.classList.contains('dark');
      }
    });
  
  
  </script>
  
  <div class="min-h-screen transition-colors duration-200 bg-white dark:bg-[#1e202a]">
    <div class="container mx-auto px-4 py-8">
      <!-- Header -->
      <div class="flex flex-col sm:flex-row sm:items-center sm:justify-between mb-8 pb-8 border-b dark:border-gray-700">
        <div>
          <h1 class="text-2xl font-bold text-gray-900 dark:text-white">Social Media Dashboard</h1>
          <p class="text-gray-600 dark:text-gray-400">Total Followers: 23,004</p>
        </div>
        <div class="flex items-center gap-2 mt-4 sm:mt-0">
          <span class="text-gray-600 dark:text-gray-400">Dark Mode</span>
          <Switch checked={isDarkMode} onCheckedChange={toggleDarkMode} />
        </div>
      </div>
  
      <!-- Main social cards -->
      <div class="flex flex-col md:flex-row gap-6 mb-12">
        {#each socialCards as card}
          <Card class="flex-1 relative overflow-hidden hover:scale-105 transition-transform duration-200">
            <div class={`h-1 absolute top-0 left-0 right-0 ${card.color}`}></div>
            <div class="p-6 flex flex-col items-center text-center">
              <div class="flex items-center gap-2 text-gray-600 dark:text-gray-400 mb-4">
                <enhanced:img src={card.icon.src} alt={card.icon.alt} />
                <span>{card.username}</span>
              </div>
              <div class="text-5xl font-bold text-gray-900 dark:text-white mb-1">{card.followers}</div>
              <div class="text-gray-500 dark:text-gray-400 tracking-[5px] text-sm mb-4">{card.followersLabel}</div>
              <div class={`flex items-center gap-1 ${card.change.type === 'up' ? 'text-green-500' : 'text-red-500'}`}>
                <span class="text-sm">{card.change.type === 'up' ? '▲' : '▼'}</span>
                <span>{card.change.value} Today</span>
              </div>
            </div>
          </Card>
        {/each}
      </div>
  
      <!-- Overview section -->
      <h2 class="text-2xl font-bold text-gray-900 dark:text-white mb-6">Overview - Today</h2>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        {#each overviewCards as card}
          <Card class="hover:scale-105 transition-transform duration-200">
            <div class="p-6">
              <div class="flex justify-between items-start mb-6">
                <span class="text-gray-600 dark:text-gray-400">{card.title}</span>
                <enhanced:img src={card.icon.src} alt={card.icon.alt} />
              </div>
              <div class="flex justify-between items-end">
                <span class="text-3xl font-bold text-gray-900 dark:text-white">{card.value}</span>
                <div class={`flex items-center gap-1 ${card.change.type === 'up' ? 'text-green-500' : 'text-red-500'}`}>
                  <span>{card.change.type === 'up' ? '▲' : '▼'}</span>
                  <span>{card.change.value}%</span>
                </div>
              </div>
            </div>
          </Card>
        {/each}
      </div>
    </div>
  </div>
  
  <style>
    @font-face {
      font-family: 'Material Symbols';
      font-style: normal;
      src: url('https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200');
    }
  </style>