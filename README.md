https://gist.github.com/subrotoice/e0738c40dae8c4ad4ce1c5786e6a1330
# Laravel-CRUDs-3Projects

1. Install Laravell, composer create-project laravel/laravel myProject
2. .env
3. Model Creation, php artisan make:model Product -mcr   // Migration, Controller with Resource, Model itself are created
4. change Model fillable
5. Change Migration
6. php artisan migrate
7. Change route
8. Change Controller 
9. Change View
10. You are good to go, php artisan serve

## Controller

    public function index()  // Display a listing of the resource, GET
    {
        $products = Product::all(); // in 3.CRUD_Mini_Product
        return view('products.index', compact('products'));
    }

    public function create()  // Show the form for creating a new resource, GET
    {
        return view('products.create');
    }

    public function store(Request $request) // Store a newly created resource in storage, POST
    {
        $data = $request->validate([
            'name' => 'required',
            'price' => 'required|integer',
            'description' => 'required'
        ]);
        Product::create($data);
        
        // Another way of doing Save
        // $product = new Product;
        // $product->name = $request->name;
        // $product->price = $request->price;
        // $product->description = $request->description;
        // $product->save();

        return redirect()->route('products.index');
    }

    public function show(Product $product) // Display the specified resource. GET
    {
        return view('products.show', compact('product'));
    }

    public function edit(Product $product) // Show the form for editing the specified resource, GET
    {
        return view('products.edit', compact('product'));
    }

    public function update(Request $request, Product $product) // Update specified in storage, PUT
    {
        $request->validate([
            'name' => 'required',
            'price' => 'required|integer',
            'description' => 'required'
        ]);
        $product->name = $request -> name;
        $product->price = $request -> price;
        $product->description = $request -> description;

        $product->save();
        return redirect()->route('products.index');
    }

    public function destroy(Product $product) // Remove the specified resource from storage, delete
    {
        $product->delete();
        return back();
    }
