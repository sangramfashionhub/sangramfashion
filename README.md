xxxxxx

export default function SangramFashionHub() {
  const [products, setProducts] = useState([]);

  const addProduct = (event) => {
    event.preventDefault();

    const name = event.target.productName.value;
    const price = event.target.productPrice.value;
    const sizes = event.target.productSizes.value.split(',').map(s => s.trim());
    const file = event.target.productImageFile.files[0];

    if (!name || !price || !sizes.length || !file) {
      alert('सर्व माहिती भरा');
      return;
    }

    const reader = new FileReader();
    reader.onload = () => {
      setProducts(prev => [...prev, { name, price, sizes, image: reader.result }]);
      event.target.reset();
    };
    reader.readAsDataURL(file);
  };

  const buyProduct = (product, size) => {
    alert(`तुम्ही ऑर्डर दिले:\n\nProduct: ${product.name}\nPrice: ₹${product.price}\nSize: ${size}\n\nधन्यवाद!`);
  };

  return (
    <div style={{ fontFamily: 'Arial', padding: '20px', backgroundColor: '#f8f8f8' }}>
      <header style={{ backgroundColor: '#ff4081', color: 'white', textAlign: 'center', padding: '20px 0' }}>
        <h1>Sangram Fashion Hub</h1>
      </header>

      <form onSubmit={addProduct} style={{ backgroundColor: 'white', padding: '15px', borderRadius: '8px', margin: '20px 0', boxShadow: '0 0 5px rgba(0,0,0,0.1)' }}>
        <input name="productName" type="text" placeholder="उत्पादनाचे नाव" style={{ width: '100%', margin: '5px 0', padding: '8px' }} />
        <input name="productPrice" type="number" placeholder="किंमत" style={{ width: '100%', margin: '5px 0', padding: '8px' }} />
        <input name="productSizes" type="text" placeholder="साईझ (S,M,L)" style={{ width: '100%', margin: '5px 0', padding: '8px' }} />
        <input name="productImageFile" type="file" accept="image/*" style={{ width: '100%', margin: '5px 0', padding: '8px' }} />
        <button type="submit" style={{ padding: '10px', backgroundColor: '#ff4081', color: 'white', border: 'none', borderRadius: '5px', cursor: 'pointer' }}>Add Product</button>
      </form>

      <div style={{ display: 'flex', flexWrap: 'wrap', gap: '20px' }}>
        {products.map((product, index) => (
          <div key={index} style={{ backgroundColor: 'white', padding: '10px', borderRadius: '8px', width: 'calc(33% - 20px)', boxShadow: '0 0 5px rgba(0,0,0,0.1)', textAlign: 'center' }}>
            <img src={product.image} alt={product.name} style={{ width: '100%', borderRadius: '5px' }} />
            <h3>{product.name}</h3>
            <p>Price: ₹{product.price}</p>
            <select>
              {product.sizes.map((size, i) => <option key={i} value={size}>{size}</option>)}
            </select>
            <button onClick={() => buyProduct(product, product.sizes[0])} style={{ marginTop: '5px', padding: '8px', width: '80%' }}>Buy Now</button>
          </div>
        ))}
      </div>
    </div>
  );
}
