<script lang="ts">
    import { _ } from 'svelte-i18n';
    import type { User as UserModel } from '../../../../stores/user';
    import { me } from '../../../../stores/me';
    import User from './user.svelte';

    interface Props {
        users: UserModel[];
    }

    let { users }: Props = $props();
</script>

<div class="users uk-flex-center uk-flex uk-text-center uk-flex-top">
    <User bind:userName={$me.name} canEdit={true} status={$_('you')} />
    {#if users}
        {#each users as user (user.id)}
            {#if $me.id !== user.id}
                <User userName={user.name} canEdit={false} status={$_('users.online')} />
            {/if}
        {/each}
    {/if}
</div>
