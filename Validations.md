# **Validations Guide**

Move validation from controllers to Request classes.

Bad:

```php
### Controller Class
public function store(Request $request)
{
    $request->validate([
        'title' => 'required|unique:posts|max:255',
        'body' => 'required',
        'publish_at' => 'nullable|date',
    ]);

    ...
}
```

Good:

```php
### Controller Class
public function store(PostRequest $request)
{
    ...
}

### Request Class
class PostRequest extends Request
{
    public function rules(): array
    {
        return [
            'title' => 'required|unique:posts|max:255',
            'body' => 'required',
            'publish_at' => 'nullable|date',
        ];
    }
}
```

### Points need to be taken care when Creating Request class
- Need to extend BaseRequest in place of FormRequest which is by default extended whenever you create Request file using artisan command.
- Need to create rules Base on route checks.

