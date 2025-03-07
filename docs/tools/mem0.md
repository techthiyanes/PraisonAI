# Mem0 and PaisonAI Integration

<iframe width="560" height="315" src="https://www.youtube.com/embed/KIGSgRxf1cY" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Mem0 is a tools to store, updated, delete and retrieve memories.
https://github.com/mem0ai/mem0

## Mem0 previously called EmbedChain

```python
from mem0 import Memory
from praisonai_tools import BaseTool

class AddMemoryTool(BaseTool):
    name: str = "Add Memory Tool"
    description: str = ("This tool allows storing a new memory with user ID and optional metadata.\n"
                        "Example:\n"
                        "   - Input: text='I am working on improving my tennis skills. Suggest some online courses.', user_id='alice', metadata={'category': 'hobbies'}\n"
                        "   - Output: Memory added with summary 'Improving her tennis skills. Looking for online suggestions.'")

    def _run(self, text: str, user_id: str, metadata: dict = None):
        m = Memory()
        result = m.add(text, user_id=user_id, metadata=metadata)
        return result

class GetAllMemoriesTool(BaseTool):
    name: str = "Get All Memories Tool"
    description: str = ("This tool retrieves all stored memories.\n"
                        "Example:\n"
                        "   - Input: action='get_all'\n"
                        "   - Output: List of all stored memories.")

    def _run(self):
        m = Memory()
        result = m.get_all()
        return result

class SearchMemoryTool(BaseTool):
    name: str = "Search Memory Tool"
    description: str = ("This tool searches for specific memories based on a query and user ID.\n"
                        "Example:\n"
                        "   - Input: query='What are Alice's hobbies?', user_id='alice'\n"
                        "   - Output: Search results related to Alice's hobbies.")

    def _run(self, query: str, user_id: str):
        m = Memory()
        result = m.search(query=query, user_id=user_id)
        return result

class UpdateMemoryTool(BaseTool):
    name: str = "Update Memory Tool"
    description: str = ("This tool updates an existing memory by memory ID and new data.\n"
                        "Example:\n"
                        "   - Input: memory_id='cb032b42-0703-4b9c-954d-77c36abdd660', data='Likes to play tennis on weekends'\n"
                        "   - Output: Memory updated to 'Likes to play tennis on weekends.'")

    def _run(self, memory_id: str, data: str):
        m = Memory()
        result = m.update(memory_id=memory_id, data=data)
        return result

class MemoryHistoryTool(BaseTool):
    name: str = "Memory History Tool"
    description: str = ("This tool gets the history of changes made to a specific memory by memory ID.\n"
                        "Example:\n"
                        "   - Input: memory_id='cb032b42-0703-4b9c-954d-77c36abdd660'\n"
                        "   - Output: History of the specified memory.")

    def _run(self, memory_id: str):
        m = Memory()
        result = m.history(memory_id=memory_id)
        return result
```