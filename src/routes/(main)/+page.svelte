<script lang="ts">
  import {
    WebsiteName,
    WebsiteBaseUrl,
    WebsiteDescription,
  } from "../../config"

  const ldJson = {
    "@context": "https://schema.org",
    "@type": "WebSite",
    name: WebsiteName,
    url: WebsiteBaseUrl,
  }
  const jsonldScript = `<script type="application/ld+json">${
    JSON.stringify(ldJson) + "<"
  }/script>`

</script>

<svelte:head>
  <title>{WebsiteName}</title>
  <meta name="description" content={WebsiteDescription} />
  <!-- eslint-disable-next-line svelte/no-at-html-tags -->
  {@html jsonldScript}
</svelte:head>

<div class="hero min-h-[60vh]">
  <div class="hero-content text-center py-12">
    <div class="max-w-xl">
      <div
        class="text-xl md:text-3xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-primary to-accent mb-4 md:mb-8"
      >
        Internet Chowkidar
      </div>

      <div
        class="text-4xl md:text-6xl font-bold px-2"
        style="line-height: 1.2;"
      >
        We
        <span
          class="underline decoration-secondary decoration-4 md:decoration-[6px]"
          >notice</span
        >
        <span
          class="underline decoration-secondary decoration-4 md:decoration-[6px]"
          >when</span
        > ISPs
        <span
          class="underline decoration-secondary decoration-4 md:decoration-[6px]"
          >block.</span
        >
      </div>
      <a
        href="/sites"
      >
        <button class="btn btn-outline btn-primary btn-lg px-6 mt-3 mx-2"
        >See what's up</button
        >
      </a>
      <div class="mt-6 md:mt-10 text-sm md:text-lg">
        Built with <a
          href="https://kit.svelte.dev"
          class="link font-bold"
          target="_blank">SvelteKit</a
        >,
        <a href="https://tailwindcss.com" class="link font-bold" target="_blank"
          >Tailwind</a
        >,
        <a href="https://go.dev" class="link font-bold" target="_blank"
        >GoLang</a
        >,
        <a href="https://daisyui.com" class="link font-bold" target="_blank"
          >DaisyUI</a
        >, and
        <a
          href="https://www.postgresql.org"
          class="link font-bold"
          target="_blank">Postgres</a
        >
      </div>
<!--      <div class="mt-6 md:mt-2">-->
<!--        <a href="https://github.com/CriticalMoments/CMSaasStarter">-->
<!--          <button class="btn btn-primary btn-sm px-6">★ us on Github</button>-->
<!--        </a>-->
<!--        <a-->
<!--          href="https://github.com/CriticalMoments/CMSaasStarter/tree/main#saas-starter"-->
<!--        >-->
<!--          <button class="btn btn-outline btn-primary btn-sm px-6 mt-3 mx-2"-->
<!--            >Read the Docs</button-->
<!--          >-->
<!--        </a>-->
<!--      </div>-->
    </div>
  </div>
</div>
<!--<div class="min-h-[60vh]">-->
<!--  <div class="pt-20 pb-8 px-7">-->
<!--    <div class="max-w-lg mx-auto text-center">-->
<!--      <div-->
<!--        class="text-3xl md:text-5xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-primary to-accent"-->
<!--      >-->
<!--        Explore the Features-->
<!--      </div>-->
<!--      <div class="mt-6 text-xl font-bold">-->
<!--        And try them on this-->
<!--        <span-->
<!--          class="underline decoration-secondary decoration-[3px] md:decoration-[4px]"-->
<!--        >-->
<!--          fully functional demo-->
<!--        </span>-->
<!--      </div>-->
<!--    </div>-->

<!--    <div-->
<!--      class="flex gap-6 mt-12 max-w-[1064px] mx-auto place-content-center flex-wrap"-->
<!--    >-->
<!--      {#each features as feature}-->
<!--        <div class="card bg-white w-[270px] min-h-[300px] flex-none shadow-xl">-->
<!--          <div class="card-body items-center text-center p-[24px] pt-[32px]">-->
<!--            <div>-->
<!--              <svg-->
<!--                width="50px"-->
<!--                height="50px"-->
<!--                class="mb-2 mt-1"-->
<!--                viewBox="0 0 24 24"-->
<!--                fill="none"-->
<!--                xmlns="http://www.w3.org/2000/svg"-->
<!--              >-->
<!--                &lt;!&ndash; eslint-disable-next-line svelte/no-at-html-tags &ndash;&gt;-->
<!--                {@html feature.svgContent}-->
<!--              </svg>-->
<!--            </div>-->
<!--            <h2 class="card-title">-->
<!--              {feature.name}-->
<!--            </h2>-->
<!--            <p class="text-sm">-->
<!--              {feature.description}-->
<!--            </p>-->
<!--            {#if feature.link}-->
<!--              <a-->
<!--                href={feature.link}-->
<!--                class="pb-4"-->
<!--                target={feature.newPage ? "_blank" : ""}-->
<!--              >-->
<!--                <button-->
<!--                  class="btn btn-xs btn-outline rounded-full btn-primary min-w-[100px]"-->
<!--                  >{feature.linkText ? feature.linkText : "Try It"}</button-->
<!--                >-->
<!--              </a>-->
<!--            {/if}-->
<!--          </div>-->
<!--        </div>-->
<!--      {/each}-->
<!--    </div>-->
<!--  </div>-->
<!--</div>-->
<!--<div class="hero min-h-[60vh] mt-12">-->
<!--  <div class="hero-content text-center pb-16 pt-4 px-4">-->
<!--    <div class="max-w-lg">-->
<!--      <div-->
<!--        class="text-3xl md:text-5xl font-bold bg-clip-text text-transparent bg-gradient-to-r from-primary to-accent mt-4"-->
<!--      >-->
<!--        See it in Action-->
<!--      </div>-->
<!--      <div-->
<!--        class="flex flex-col lg:flex-row mt-8 gap-6 place-content-center content-center"-->
<!--      >-->
<!--        <div class="hidden md:block">-->
<!--          <a href="https://criticalmoments.io" target="_blank" class="link">-->
<!--            <div class="mockup-browser border">-->
<!--              <div class="mockup-browser-toolbar">-->
<!--                <div class="input" style="background:#eee;">-->
<!--                  https://criticalmoments.io-->
<!--                </div>-->
<!--              </div>-->
<!--              <div class="flex justify-center">-->
<!--                <img-->
<!--                  alt="Screenshot of criticalmoments.io homepage"-->
<!--                  class="aspect-[2044/1242]"-->
<!--                  src="/images/example-home.png"-->
<!--                />-->
<!--              </div>-->
<!--            </div>-->
<!--          </a>-->
<!--        </div>-->
<!--        <div class="md:hidden">-->
<!--          <a href="https://criticalmoments.io" target="_blank" class="link">-->
<!--            <div class="card shadow-xl border overflow-hidden">-->
<!--              <img-->
<!--                alt="Screenshot of criticalmoments.io homepage"-->
<!--                class="aspect-[2044/1242]"-->
<!--                src="/images/example-home.png"-->
<!--              />-->
<!--            </div></a-->
<!--          >-->
<!--        </div>-->
<!--        <div class="min-w-[270px] lg:min-w-[420px] flex mt-6 lg:mt-0">-->
<!--          <div class="my-auto">-->
<!--            <div class="px-4 text-lg md:text-xl">-->
<!--              <a href="https://criticalmoments.io" class="" target="_blank"-->
<!--                >SaaS Starter was created by <span-->
<!--                  class="font-bold whitespace-nowrap">Critical Moments</span-->
<!--                >: a SDK to to help mobile apps-->
<!--                <span class="underline decoration-secondary decoration-[3px]"-->
<!--                  >increase conversion rates and app-ratings.</span-->
<!--                ></a-->
<!--              >-->
<!--            </div>-->
<!--            <div class="px-4 mt-6 text-lg md:text-xl">-->
<!--              Our <a-->
<!--                href="https://criticalmoments.io"-->
<!--                class="link font-bold"-->
<!--                target="_blank">webpage</a-->
<!--              > is the best example of SaaS Starter with style and real content.-->
<!--            </div>-->
<!--            <div class="mt-4 text-large">-->
<!--              <a href="https://criticalmoments.io" target="_blank">-->
<!--                <button class="btn btn-primary btn-wide mt-3"-->
<!--                  >See it in Action</button-->
<!--                >-->
<!--              </a>-->
<!--            </div>-->
<!--          </div>-->
<!--        </div>-->
<!--      </div>-->
<!--    </div>-->
<!--  </div>-->
<!--</div>-->
