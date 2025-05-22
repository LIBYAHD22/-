# -
مسلسل تركي 
<!DOCTYPE html>
<html lang="ar">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <title>مسلسلات وأفلام تركية</title>
  <style>
    body { font-family: Arial, sans-serif; direction: rtl; background: #f5f5f5; margin: 0; padding: 0; }
    header { background: #d32f2f; color: white; padding: 15px; text-align: center; }
    main { padding: 20px; max-width: 900px; margin: auto; }
    .search-box { margin-bottom: 20px; }
    input[type="text"] {
      width: 100%; padding: 10px; font-size: 16px; border: 1px solid #ccc; border-radius: 5px;
    }
    .media-list { display: grid; grid-template-columns: repeat(auto-fill, minmax(180px, 1fr)); gap: 15px; }
    .media-item {
      background: white; border-radius: 8px; box-shadow: 0 2px 5px rgb(0 0 0 / 0.1);
      overflow: hidden; cursor: pointer; transition: transform 0.2s;
    }
    .media-item:hover { transform: scale(1.05); }
    .media-item img { width: 100%; height: 270px; object-fit: cover; }
    .media-info { padding: 10px; }
    .media-title { font-weight: bold; margin-bottom: 5px; }
    .media-type { font-size: 14px; color: #666; }
    .details {
      background: white; max-width: 700px; margin: 20px auto; padding: 15px; border-radius: 8px; box-shadow: 0 2px 8px rgba(0,0,0,0.2);
    }
    .details h2 { margin-top: 0; }
    .back-button {
      background: #d32f2f; color: white; border: none; padding: 8px 15px; border-radius: 5px; cursor: pointer;
      margin-bottom: 10px;
    }
  </style>
</head>
<body>

<header>
  <h1>مسلسلات وأفلام تركية</h1>
</header>

<main>
  <div class="search-box">
    <input type="text" id="searchInput" placeholder="ابحث عن مسلسل أو فيلم..." />
  </div>

  <div id="mediaList" class="media-list"></div>

  <div id="detailsView" style="display:none;"></div>
</main>

<script>
  // بيانات وهمية (ممكن تبدلها لاحقاً بAPI)
  const mediaData = [
    {
      id: 1,
      title: "قيامة أرطغرل",
      type: "مسلسل",
      year: 2014,
      description: "مسلسل تاريخي يتحدث عن حياة أرطغرل والد عثمان الأول مؤسس الدولة العثمانية.",
      image: "https://upload.wikimedia.org/wikipedia/en/7/7f/Dirilis_Ertugrul.jpg"
    },
    {
      id: 2,
      title: "العشق الممنوع",
      type: "مسلسل",
      year: 2008,
      description: "قصة حب درامية معقدة بين عائلات مختلفة في تركيا.",
      image: "https://upload.wikimedia.org/wikipedia/en/f/f9/Ashk_Mamnuh.jpg"
    },
    {
      id: 3,
      title: "فيلم وصمة عار",
      type: "فيلم",
      year: 2017,
      description: "فيلم درامي يتناول مواضيع اجتماعية حساسة في المجتمع التركي.",
      image: "https://upload.wikimedia.org/wikipedia/en/4/4c/Headscarft_film_poster.jpg"
    },
    {
      id: 4,
      title: "فيلم صوفيا",
      type: "فيلم",
      year: 2018,
      description: "فيلم درامي رومانسي عن قصة حب وصراعات شخصية.",
      image: "https://upload.wikimedia.org/wikipedia/en/2/2f/Sofia_film_poster.jpg"
    }
  ];

  const mediaListEl = document.getElementById('mediaList');
  const detailsViewEl = document.getElementById('detailsView');
  const searchInput = document.getElementById('searchInput');

  function renderList(data) {
    detailsViewEl.style.display = 'none';
    mediaListEl.style.display = 'grid';

    mediaListEl.innerHTML = '';

    if (data.length === 0) {
      mediaListEl.innerHTML = '<p>لا توجد نتائج.</p>';
      return;
    }

    data.forEach(item => {
      const div = document.createElement('div');
      div.className = 'media-item';
      div.innerHTML = `
        <img src="${item.image}" alt="${item.title}" />
        <div class="media-info">
          <div class="media-title">${item.title}</div>
          <div class="media-type">${item.type} - ${item.year}</div>
        </div>
      `;
      div.onclick = () => showDetails(item.id);
      mediaListEl.appendChild(div);
    });
  }

  function showDetails(id) {
    const item = mediaData.find(m => m.id === id);
    if (!item) return;

    mediaListEl.style.display = 'none';
    detailsViewEl.style.display = 'block';

    detailsViewEl.innerHTML = `
      <button class="back-button" onclick="renderList(mediaData)">عودة</button>
      <h2>${item.title}</h2>
      <img src="${item.image}" alt="${item.title}" style="width:100%; max-height:400px; object-fit:cover; border-radius:8px;" />
      <p><strong>النوع:</strong> ${item.type}</p>
      <p><strong>السنة:</strong> ${item.year}</p>
      <p><strong>الوصف:</strong> ${item.description}</p>
    `;
  }

  searchInput.addEventListener('input', () => {
    const query = searchInput.value.trim().toLowerCase();
    const filtered = mediaData.filter(item => item.title.toLowerCase().includes(query));
    renderList(filtered);
  });

  // عرض القائمة الأولية
  renderList(mediaData);
</script>

</body>
</html>
