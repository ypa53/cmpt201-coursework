#include <stdint.h>
#include <stdio.h>
#include <stdlib.h>

struct header {
  uint64_t size;
  struct header *next;
  int id;
};

void initialize_block(struct header *block, uint64_t size, struct header *next,
                      int id) {
  block->size = size;
  block->next = next;
  block->id = id;
}

int find_first_fit(struct header *free_list_ptr, uint64_t size) {
  struct header *cur = free_list_ptr;
  while (cur) {
    if (cur->size >= size)
      return cur->id;
    cur = cur->next;
  }
  return -1;
}

int find_best_fit(struct header *free_list_ptr, uint64_t size) {
  struct header *cur = free_list_ptr;
  int best_id = -1;
  uint64_t best_size = UINT64_MAX;

  while (cur) {
    if (cur->size >= size && cur->size < best_size) {
      best_size = cur->size;
      best_id = cur->id;
    }
    cur = cur->next;
  }
  return best_id;
}

int find_worst_fit(struct header *free_list_ptr, uint64_t size) {
  struct header *cur = free_list_ptr;
  int worst_id = -1;
  uint64_t worst_size = 0;

  while (cur) {
    if (cur->size >= size && cur->size > worst_size) {
      worst_size = cur->size;
      worst_id = cur->id;
    }
    cur = cur->next;
  }
  return worst_id;
}

int main(void) {
  struct header *free_block1 = malloc(sizeof(struct header));
  struct header *free_block2 = malloc(sizeof(struct header));
  struct header *free_block3 = malloc(sizeof(struct header));
  struct header *free_block4 = malloc(sizeof(struct header));
  struct header *free_block5 = malloc(sizeof(struct header));

  initialize_block(free_block1, 6, free_block2, 1);
  initialize_block(free_block2, 12, free_block3, 2);
  initialize_block(free_block3, 24, free_block4, 3);
  initialize_block(free_block4, 8, free_block5, 4);
  initialize_block(free_block5, 4, NULL, 5);

  struct header *free_list_ptr = free_block1;

  int first_fit_id = find_first_fit(free_list_ptr, 7);
  int best_fit_id = find_best_fit(free_list_ptr, 7);
  int worst_fit_id = find_worst_fit(free_list_ptr, 7);

  printf("The ID for First-Fit algorithm is: %d\n", first_fit_id);
  printf("The ID for Best-Fit algorithm is: %d\n", best_fit_id);
  printf("The ID for Worst-Fit algorithm is: %d\n", worst_fit_id);

  free(free_block1);
  free(free_block2);
  free(free_block3);
  free(free_block4);
  free(free_block5);

  return 0;
}

/* Pseudocode: Coalescing Contiguous Free Blocks

function coalesce(free_list_head, new_block):
  prev = NULL
  cur = free_list_head

  while (cur != NULL and cur < new_block):
      prev = cur
      cur = cur.next

  new_block.next = cur
  if prev != NULL:
      prev.next = new_block
  else:
      free_list_head = new_block

  if (prev != NULL and prev is adjacent to new_block):
      prev.size += new_block.size
      prev.next = new_block.next
      new_block = prev

  if (new_block.next != NULL and new_block is adjacent to new_block.next):
      new_block.size += new_block.next.size
      new_block.next = new_block.next.next

  return free_list_head
*/
