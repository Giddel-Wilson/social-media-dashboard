<script lang="ts">
  import { Card } from "$lib/components/ui/card";
  import { Switch } from "$lib/components/ui/switch";
  import { browser } from "$app/environment";
  import { onMount } from "svelte";
  import facebookIcon from "$lib/assets/facebook.svg";
  import twitterIcon from "$lib/assets/twitter.svg";
  import instagramIcon from "$lib/assets/instagram.svg";
  import youtubeIcon from "$lib/assets/youtube.svg";
  import NumberTicker from "$lib/components/magic/ NumberTicker.svelte";
  import { isDarkMode } from "$lib/utils";

  // Social media stats data

  const socialCards = [
    {
      platform: "facebook",
      username: "@nathanf",
      followers: "1987",
      followersLabel: "FOLLOWERS",
      change: { value: 12, type: "up" },
      color: "bg-blue-500",
      icon: { src: facebookIcon, alt: "Facebook" },
    },
    {
      platform: "twitter",
      username: "@nathanf",
      followers: "1044",
      followersLabel: "FOLLOWERS",
      change: { value: 99, type: "up" },
      color: "bg-blue-400",
      icon: { src: twitterIcon, alt: "Twitter" },
    },
    {
      platform: "instagram",
      username: "@realnathanf",
      followers: "11k",
      followersLabel: "FOLLOWERS",
      change: { value: 1099, type: "up" },
      color: "bg-gradient-to-r from-yellow-400 via-pink-500 to-pink-600",
      icon: { src: instagramIcon, alt: "Instagram" },
    },
    {
      platform: "youtube",
      username: "Nathan F.",
      followers: "8239",
      followersLabel: "SUBSCRIBERS",
      change: { value: 144, type: "down" },
      color: "bg-red-600",
      icon: { src: youtubeIcon, alt: "YouTube" },
    },
  ];

  const overviewCards = [
    {
      title: "Page Views",
      platform: "facebook",
      value: "87",
      change: { value: 3, type: "up" },
      icon: { src: facebookIcon, alt: "Facebook" },
    },
    {
      title: "Likes",
      platform: "facebook",
      value: "52",
      change: { value: 2, type: "down" },
      icon: { src: facebookIcon, alt: "Facebook" },
    },
    {
      title: "Likes",
      platform: "instagram",
      value: "5462",
      change: { value: 2257, type: "up" },
      icon: { src: instagramIcon, alt: "Instagram" },
    },
    {
      title: "Profile Views",
      platform: "instagram",
      value: "52000",
      change: { value: 1375, type: "up" },
      icon: { src: instagramIcon, alt: "Instagram" },
    },
    {
      title: "Retweets",
      platform: "twitter",
      value: "117",
      change: { value: 303, type: "up" },
      icon: { src: twitterIcon, alt: "Twitter" },
    },
    {
      title: "Likes",
      platform: "twitter",
      value: "507",
      change: { value: 553, type: "up" },
      icon: { src: twitterIcon, alt: "Twitter" },
    },
    {
      title: "Likes",
      platform: "youtube",
      value: "107",
      change: { value: 19, type: "down" },
      icon: { src: youtubeIcon, alt: "YouTube" },
    },
    {
      title: "Total Views",
      platform: "youtube",
      value: "1407",
      change: { value: 12, type: "down" },
      icon: { src: youtubeIcon, alt: "YouTube" },
    },
  ];

  function toggleDarkMode() {
    isDarkMode.set(!$isDarkMode);
    if (browser) {
      document.documentElement.classList.toggle("dark");
    }
  }

  onMount(() => {
    if (browser) {
      $isDarkMode == true && document.documentElement.classList.add("dark");
    }
  });
</script>

<div
  class="min-h-screen bg-white transition-colors duration-200 dark:bg-[#1e202a]"
>
  <div class="container mx-auto px-4 py-8">
    <!-- Header -->
    <div
      class="mb-8 flex flex-col border-b pb-8 dark:border-gray-700 sm:flex-row sm:items-center sm:justify-between"
    >
      <div>
        <h1 class="text-2xl font-bold text-gray-900 dark:text-white">
          Social Media Dashboard
        </h1>
        <div class="text-gray-600 dark:text-gray-400">
          Total Followers:
          <span class="font-bold">
            <NumberTicker
              withCommas={true}
              value={23004}
              initial={0}
              duration={3000}
            />
          </span>
        </div>
      </div>
      <div class="mt-4 flex items-center gap-2 sm:mt-0">
        <span class="text-gray-600 dark:text-gray-400">Dark Mode</span>
        <Switch checked={$isDarkMode} onCheckedChange={toggleDarkMode} />
      </div>
    </div>

    <!-- Main social cards -->
    <div class="mb-12 flex flex-col gap-6 md:flex-row">
      {#each socialCards as card, i}
        <Card
          class="relative flex-1 overflow-hidden transition-transform duration-200 hover:scale-105"
        >
          <div class={`h-1 absolute top-0 left-0 right-0 ${card.color}`}></div>
          <div class="flex flex-col items-center p-6 text-center">
            <div
              class="mb-4 flex items-center gap-2 text-gray-600 dark:text-gray-400"
            >
              <img src={card.icon.src} alt={card.icon.alt} />
              <span>{card.username}</span>
            </div>
            <div class="mb-1 text-5xl font-bold text-gray-900 dark:text-white">
              {card.followers}
            </div>
            <div
              class="mb-4 text-sm tracking-[5px] text-gray-500 dark:text-gray-400"
            >
              {card.followersLabel}
            </div>
            <div
              class={`flex items-center gap-1 ${card.change.type === "up" ? "text-green-500" : "text-red-500"}`}
            >
              <span class="text-sm"
                >{card.change.type === "up" ? "▲" : "▼"}</span
              >
              <span> <NumberTicker value={card.change.value} /> Today</span>
            </div>
          </div>
        </Card>
      {/each}
    </div>

    <!-- Overview section -->
    <h2 class="mb-6 text-2xl font-bold text-gray-900 dark:text-white">
      Overview - Today
    </h2>
    <div class="grid grid-cols-1 gap-6 md:grid-cols-2 lg:grid-cols-4">
      {#each overviewCards as card, i}
        <Card class="transition-transform duration-200 hover:scale-105">
          <div class="p-6">
            <div class="mb-6 flex items-start justify-between">
              <span class="text-gray-600 dark:text-gray-400">{card.title}</span>
              <img src={card.icon.src} alt={card.icon.alt} />
            </div>
            <div class="flex items-end justify-between">
              <span class="text-3xl font-bold text-gray-900 dark:text-white">
                <NumberTicker
                  value={Number(card.value)}
                  duration={3000 + 3 * i}
                />
              </span>
              <div
                class={`flex items-center gap-1 ${card.change.type === "up" ? "text-green-500" : "text-red-500"}`}
              >
                <span>{card.change.type === "up" ? "▲" : "▼"}</span>
                <span> <NumberTicker value={card.change.value} />%</span>
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
    font-family: "Material Symbols";
    font-style: normal;
    src: url("https://fonts.googleapis.com/css2?family=Material+Symbols+Outlined:opsz,wght,FILL,GRAD@20..48,100..700,0..1,-50..200");
  }
</style>
