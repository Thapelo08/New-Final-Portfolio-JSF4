<template>
  <button @click.stop="toggleWishlist" class="focus:outline-none">
    <svg xmlns="http://www.w3.org/2000/svg" fill="currentColor" :class="{'text-gray-300': !isInWishlist, 'text-red-500': isInWishlist}" class="w-6 h-6" viewBox="0 0 24 24">
      <path d="M12 21.35l-1.45-1.32C5.4 15.36 2 12.28 2 8.5 2 5.42 4.42 3 7.5 3c1.74 0 3.41.81 4.5 2.09C13.09 3.81 14.76 3 16.5 3 19.58 3 22 5.42 22 8.5c0 3.78-3.4 6.86-8.55 11.54L12 21.35z"/>
    </svg>
  </button>
</template>

<script>
import { computed } from 'vue';
import { useWishlist } from '../composables/useWishlist';

export default {
  name: 'WishlistButton',
  props: {
    productId: {
      type: Number,
      required: true,
    },
  },
  setup(props) {
    const { wishlist, addToWishlist, removeFromWishlist } = useWishlist();

    const isInWishlist = computed(() => wishlist.value.some(item => item.id === props.productId));

    const toggleWishlist = () => {
      if (isInWishlist.value) {
        removeFromWishlist(props.productId);
      } else {
        addToWishlist(props.productId);
      }
    };

    return {
      isInWishlist,
      toggleWishlist,
    };
  },
};
</script>