<script>
  export let visible = false
  export let code
  export let type
  export let onClick
  export let data
  export let onUpdateGuideline

  import Dialog from '@fouita/dialog'
  // import { currentUser } from '../../../stores/current_user'
  import DataField from './DataField.svelte'

  //   onMount(() => {
  //     console.log('mount')
  //   })

  // const getComment = Functions.httpsCallable('getComment')
  let isLoading = false
  let upload = false

  //   $: {
  //     if (visible) {
  //         isLoading = false
  //         if (d.data) {
  //           if (d.data.likert) likert = +d.data.likert
  //           if (d.data.GUIDELINE) GUIDELINE = d.data.GUIDELINE
  //           if (d.data.CHECK) CHECK = d.data.CHECK
  //         }
  //       })
  //     }
  //     // console.log('currentUser', $currentUser)
  //   }
  const onUpload = (e, obj) => {
    upload = e
    const c = { code, ...obj }
    console.log('c', c)
    onUpdateGuideline(c)
  }
</script>

<Dialog inverted color="indigo" rounded="sm" bind:visible title="Comment: {code}" closable={false}>
  <div class="relative">
    {#if isLoading}
      <p class="absolute m-auto text-xl" style="top: 50%; left:40%">Loading...</p>
    {/if}
    <form class="flex flex-col m-2 {isLoading && 'opacity-0'}">
      <div class="flex flex-col">
        <DataField {type} {code} {onUpload} {data} />
      </div>
      <button
        disabled={upload}
        class="mx-2 mt-1 mb-2 p-1 bg-indigo-100 text-indigo-900 font-bold"
        on:click|preventDefault={() => {
          onClick()
          // isLoading = true
        }}>{upload ? 'Updating...' : 'Close'}</button>
    </form>
  </div>
</Dialog>
