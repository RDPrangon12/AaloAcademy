<script>
import {
    onDestroy
} from "svelte"
import {Footer} from '../components'
import store from "../database/store"

const divH = window.innerHeight - 135;

let data = {};
const unsub = store.subscribe(db => {
    data = db.blog;
})

onDestroy(() => {
    unsub();
})
</script>

<section class="text-gray-600 body-font overflow-hidden">
    <div style="height: {divH}px; width-auto" class="container lg:px-24 px-5 py-10 lg:py-16 mx-auto overflow-y-auto overflow-x-hidden">
        <div class="flex flex-wrap -m-12">

            {#each data as post}
            <div class="p-12 md:w-1/2 flex flex-col items-start">
                <span class="inline-block py-1 px-2 rounded bg-red-50 text-primary text-xs font-medium tracking-widest">{post.topic}</span>
                <h2 class="sm:text-3xl text-2xl title-font font-medium text-gray-900 mt-4 mb-4">{post.head}</h2>
                <p class="leading-relaxed mb-8 text-justify">{post.body}</p>
                <div class="flex items-center flex-wrap pb-4 mb-4 border-b-2 border-gray-100 mt-auto w-full">
                    <a href={post.fbLink} target='_blank' class="text-primary inline-flex items-center">Read More
                        <svg class="w-4 h-4 ml-2" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2" fill="none" stroke-linecap="round" stroke-linejoin="round">
                            <path d="M5 12h14"></path>
                            <path d="M12 5l7 7-7 7"></path>
                        </svg>
                    </a>
                </div>
                <a href={post.fbProfile} target='_blank' class="inline-flex items-center">
                    <img alt="dp" src={`/images/blog/dp/${post.image}.jpg`} class="w-12 h-12 rounded-full flex-shrink-0 object-cover object-center">
                    <span class="flex-grow flex flex-col pl-4">
                        <span class="title-font font-medium text-gray-900">{post.author}</span>
                        <span class="text-gray-400 text-xs tracking-widest mt-0.5">{post.rank}</span>
                    </span>
                </a>
            </div>
            {/each}

        </div>
        <div class="mb-5 lg:mb-0"> <Footer /></div>
    </div>

</section>
