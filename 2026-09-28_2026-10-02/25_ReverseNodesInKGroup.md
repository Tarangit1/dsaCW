# 25. Reverse Nodes in k-Group

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode* reverseKGroup(ListNode* head, int k) {
        if (!head || k == 1) return head;

        ListNode dummy(0);
        dummy.next = head;

        ListNode* pre = &dummy;
        ListNode* end = &dummy;

        while (end->next) {
            for (int i = 0; i < k && end; i++) {
                end = end->next;
            }

            if (!end) break;

            ListNode* start = pre->next;
            ListNode* nextGroup = end->next;

            end->next = nullptr;
            pre->next = reverse(start);

            while (pre->next) {
                pre = pre->next;
            }

            pre->next = nextGroup;
            end = pre;
        }

        return dummy.next;
    }

private:
    ListNode* reverse(ListNode* head) {
        ListNode* prev = nullptr;
        ListNode* curr = head;

        while (curr) {
            ListNode* nextNode = curr->next;
            curr->next = prev;
            prev = curr;
            curr = nextNode;
        }

        return prev;
    }
};
```
