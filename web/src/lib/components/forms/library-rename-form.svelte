<script lang="ts">
  import type { LibraryResponseDto } from '@immich/sdk';
  import { Button, Field, Input, Modal, ModalBody, ModalFooter } from '@immich/ui';
  import { mdiRenameOutline } from '@mdi/js';
  import { t } from 'svelte-i18n';

  interface Props {
    library: Partial<LibraryResponseDto>;
    onCancel: () => void;
    onSubmit: (library: Partial<LibraryResponseDto>) => void;
  }

  let { library, onCancel, onSubmit }: Props = $props();

  let newName = $state(library.name);

  const onsubmit = (event: Event) => {
    event.preventDefault();
    onSubmit({ ...library, name: newName });
  };
</script>

<Modal icon={mdiRenameOutline} title={$t('rename')} onClose={onCancel} size="small">
  <ModalBody>
    <form {onsubmit} autocomplete="off" id="rename-library-form">
      <Field label={$t('name')}>
        <Input bind:value={newName} />
      </Field>
    </form>
  </ModalBody>

  <ModalFooter>
    <div class="flex gap-2 w-full">
      <Button shape="round" fullWidth color="secondary" onclick={onCancel}>{$t('cancel')}</Button>
      <Button shape="round" fullWidth type="submit" form="rename-library-form">{$t('save')}</Button>
    </div>
  </ModalFooter>
</Modal>
