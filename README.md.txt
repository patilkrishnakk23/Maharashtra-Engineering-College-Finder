<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Maharashtra College Finder</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.4.0/css/all.min.css">
    <style>
        .fade-in {
            animation: fadeIn 0.5s ease-in;
        }
        @keyframes fadeIn {
            from { opacity: 0; }
            to { opacity: 1; }
        }
        .card-hover {
            transition: transform 0.3s ease, box-shadow 0.3s ease;
        }
        .card-hover:hover {
            transform: translateY(-5px);
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
        }
        .dropdown-content {
            display: none;
            position: absolute;
            z-index: 1;
        }
        .dropdown:hover .dropdown-content {
            display: block;
        }
    </style>
</head>
<body class="bg-gray-50">
    <div class="min-h-screen">
        <!-- Header -->
        <header class="bg-gradient-to-r from-blue-600 to-indigo-800 text-white shadow-lg">
            <div class="container mx-auto px-4 py-8">
                <div class="flex flex-col md:flex-row justify-between items-center">
                    <div class="mb-6 md:mb-0">
                        <h1 class="text-3xl font-bold">Maharashtra Engineering College Finder</h1>
                        <p class="mt-2">Find the perfect college for AI/ML and Data Science programs</p>
                    </div>
                    <div class="flex items-center">
                        <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/ca397f28-a0c4-4f8b-ab7a-fca82dae8f57.png" alt="Maharashtra state outline with educational building icons representing colleges across the region" class="h-16">
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <main class="container mx-auto px-4 py-8">
            <!-- Search Section -->
            <section class="bg-white rounded-lg shadow-md p-6 mb-8 fade-in">
                <div class="flex flex-col md:flex-row gap-4 items-end">
                    <div class="flex-1">
                        <label for="percentile" class="block text-sm font-medium text-gray-700 mb-1">Enter Your MHTCET Percentile</label>
                        <div class="flex items-center">
                            <input type="number" id="percentile" min="0" max="100" step="0.01"
                                class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500"
                                placeholder="e.g., 85.76">
                            <span class="ml-2 text-gray-500">%</span>
                        </div>
                    </div>
                    <div class="flex-1">
                        <label for="region" class="block text-sm font-medium text-gray-700 mb-1">Select Region</label>
                        <select id="region" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
                            <option value="all">All Maharashtra</option>
                            <option value="pune" selected>Pune Region</option>
                            <option value="mumbai">Mumbai Region</option>
                            <option value="nagpur">Nagpur Region</option>
                            <option value="aurangabad">Aurangabad Region</option>
                        </select>
                    </div>
                    <div class="flex-1">
                        <label for="branch" class="block text-sm font-medium text-gray-700 mb-1">Prefered Branch</label>
                        <select id="branch" class="w-full px-4 py-2 border border-gray-300 rounded-lg focus:ring-2 focus:ring-blue-500 focus:border-blue-500">
                            <option value="all">All Engineering Branches</option>
                            <option value="ai_ml" selected>AI/ML</option>
                            <option value="ai_ds">AI & Data Science</option>
                            <option value="computer">Computer Engineering</option>
                        </select>
                    </div>
                    <button id="search-btn" class="bg-blue-600 hover:bg-blue-700 text-white font-medium py-2 px-6 rounded-lg transition-colors duration-200 whitespace-nowrap">
                        Find Colleges <i class="fas fa-search ml-2"></i>
                    </button>
                </div>
            </section>

            <!-- Results Section -->
            <section id="results-section" class="hidden">
                <div class="flex justify-between items-center mb-6">
                    <h2 class="text-2xl font-semibold text-gray-800">Recommended Colleges</h2>
                    <div class="dropdown relative">
                        <button class="bg-white border border-gray-300 px-4 py-2 rounded-lg flex items-center">
                            <span>Sort By</span>
                            <i class="fas fa-chevron-down ml-2"></i>
                        </button>
                        <div class="dropdown-content mt-1 w-48 bg-white shadow-lg rounded-lg overflow-hidden">
                            <button class="sort-btn w-full text-left px-4 py-2 hover:bg-gray-100" data-sort="percentile_high">Highest Cutoff First</button>
                            <button class="sort-btn w-full text-left px-4 py-2 hover:bg-gray-100" data-sort="percentile_low">Lowest Cutoff First</button>
                            <button class="sort-btn w-full text-left px-4 py-2 hover:bg-gray-100" data-sort="name_asc">A-Z</button>
                            <button class="sort-btn w-full text-left px-4 py-2 hover:bg-gray-100" data-sort="name_desc">Z-A</button>
                        </div>
                    </div>
                </div>

                <div id="results-container" class="grid gap-6 md:grid-cols-2 lg:grid-cols-3">
                    <!-- Results will be inserted here by JavaScript -->
                </div>

                <div id="no-results" class="hidden text-center py-12">
                    <img src="https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/d6873346-030a-4a89-93f4-28ed21b9a24b.png" alt="Illustration of a magnifying glass over a document with a sad face, indicating no results found" class="mx-auto mb-4">
                    <h3 class="text-xl font-medium text-gray-600">No colleges found matching your criteria</h3>
                    <p class="text-gray-500">Try adjusting your percentile or branch preference</p>
                </div>
            </section>

            <!-- CAP Round Information Section -->
            <section id="cap-info" class="hidden bg-white rounded-lg shadow-md p-6 mt-8 fade-in">
                <h2 class="text-2xl font-semibold text-gray-800 mb-4">About CAP Rounds</h2>
                <div class="grid md:grid-cols-3 gap-6">
                    <div class="bg-blue-50 p-4 rounded-lg">
                        <h3 class="font-medium text-blue-800 mb-2">Round 1</h3>
                        <p class="text-gray-700">Initial allotment based on merit and preferences. Usually conducted in July.</p>
                    </div>
                    <div class="bg-purple-50 p-4 rounded-lg">
                        <h3 class="font-medium text-purple-800 mb-2">Round 2</h3>
                        <p class="text-gray-700">Second allotment for remaining seats. Typically in August.</p>
                    </div>
                    <div class="bg-green-50 p-4 rounded-lg">
                        <h3 class="font-medium text-green-800 mb-2">Round 3</h3>
                        <p class="text-gray-700">Final round for leftover seats and special cases. Occurs in September.</p>
                    </div>
                </div>
            </section>
        </main>

        <!-- Footer -->
        <footer class="bg-gray-800 text-white py-8">
            <div class="container mx-auto px-4">
                <div class="flex flex-col md:flex-row justify-between items-center">
                    <div class="mb-4 md:mb-0">
                        <h2 class="text-xl font-bold mb-2">Maharashtra College Finder</h2>
                        <p class="text-gray-400">Find your perfect engineering college</p>
                    </div>
                    <div class="flex space-x-4">
                        <a href="#" class="hover:text-blue-400 transition-colors"><i class="fab fa-github fa-lg"></i></a>
                        <a href="#" class="hover:text-blue-400 transition-colors"><i class="fas fa-envelope fa-lg"></i></a>
                    </div>
                </div>
                <div class="border-t border-gray-700 mt-6 pt-6 text-center text-gray-400 text-sm">
                    <p>© 2023 College Finder. Data is based on previous year CAP rounds. For official information, visit <a href="https://mhtcet2023.mahacet.org" class="text-blue-400 hover:underline">MHTCET website</a>.</p>
                </div>
            </div>
        </footer>
    </div>

    <script>
        // Sample dataset - in a real app, this would come from an API or file
        const collegesData = [
            {
                id: 1,
                name: "College of Engineering, Pune",
                location: "Pune",
                branch: "AI/ML",
                round1: 98.5,
                round2: 97.8,
                round3: 96.2,
                fees: 125000,
                rating: 4.7,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0d28b388-672d-46ad-bb78-f5ec84650f50.png",
                alt: "Historic building of College of Engineering Pune with red brick architecture and green lawns",
                website: "https://www.coep.org.in"
            },
            {
                id: 2,
                name: "Vishwakarma Institute of Technology",
                location: "Pune",
                branch: "AI & Data Science",
                round1: 95.2,
                round2: 94.1,
                round3: 92.7,
                fees: 145000,
                rating: 4.5,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/40942ea2-01fd-4e39-a650-9f51676fc707.png",
                alt: "Modern campus building of Vishwakarma Institute with glass facade and students walking",
                website: "https://www.vit.edu"
            },
            {
                id: 3,
                name: "Pune Institute of Computer Technology",
                location: "Pune",
                branch: "AI/ML",
                round1: 93.8,
                round2: 92.5,
                round3: 90.3,
                fees: 135000,
                rating: 4.3,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/0c7bc4ba-65fb-44cd-b2c6-33c82411966b.png",
                alt: "PICT campus view showing academic buildings and computer lab facilities",
                website: "https://www.pict.edu"
            },
            {
                id: 4,
                name: "Maharashtra Institute of Technology",
                location: "Pune",
                branch: "AI & Data Science",
                round1: 91.5,
                round2: 90.2,
                round3: 88.7,
                fees: 150000,
                rating: 4.2,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/92f7d8ca-9842-4b6c-92b8-cf5a40e3648e.png",
                alt: "Main entrance of MIT Pune with its distinctive red and white architecture",
                website: "https://www.mitpune.com"
            },
            {
                id: 5,
                name: "Army Institute of Technology",
                location: "Pune",
                branch: "Computer Engineering",
                round1: 96.8,
                round2: 95.5,
                round3: 93.9,
                fees: 120000,
                rating: 4.6,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/190d2777-b121-445f-b793-c022363e6438.png",
                alt: "Well-maintained campus of AIT with military precision and sports facilities",
                website: "https://www.aitpune.com"
            },
            {
                id: 6,
                name: "DY Patil College of Engineering",
                location: "Pune",
                branch: "AI/ML",
                round1: 89.7,
                round2: 88.3,
                round3: 86.5,
                fees: 160000,
                rating: 4.0,
                image: "https://storage.googleapis.com/workspace-0f70711f-8b4e-4d94-86f1-2a93ccde5887/image/41e0fc43-e993-4d4b-b504-9fe611edcb72.png",
                alt: "Modern DY Patil campus with contemporary architecture and green spaces",
                website: "https://www.dypcoeakurdi.ac.in"
            }
        ];

        // DOM Elements
        const searchBtn = document.getElementById('search-btn');
        const resultsSection = document.getElementById('results-section');
        const resultsContainer = document.getElementById('results-container');
        const noResultsDiv = document.getElementById('no-results');
        const capInfoSection = document.getElementById('cap-info');

        // Event Listeners
        searchBtn.addEventListener('click', handleSearch);
        document.querySelectorAll('.sort-btn').forEach(btn => {
            btn.addEventListener('click', handleSort);
        });

        // Search Handler
        function handleSearch() {
            const percentile = parseFloat(document.getElementById('percentile').value);
            const region = document.getElementById('region').value;
            const branch = document.getElementById('branch').value;

            if (isNaN(percentile) || percentile < 0 || percentile > 100) {
                alert('Please enter a valid percentile between 0 and 100');
                return;
            }

            // Filter colleges based on inputs
            let filteredColleges = collegesData.filter(college => {
                // Filter by region if not 'all'
                if (region !== 'all' && college.location.toLowerCase() !== region) {
                    return false;
                }

                // Filter by branch if not 'all'
                if (branch !== 'all' && 
                    (branch === 'ai_ml' ? college.branch !== 'AI/ML' : 
                     branch === 'ai_ds' ? college.branch !== 'AI & Data Science' : 
                     college.branch !== 'Computer Engineering')) {
                    return false;
                }

                return true;
            });

            // Mark eligible colleges (within 5% range)
            filteredColleges = filteredColleges.map(college => {
                const cutoff = Math.min(college.round1, college.round2, college.round3);
                const isEligible = percentile >= cutoff - 5;
                return { ...college, isEligible };
            });

            // Sort by how close the percentile is to cutoff
            filteredColleges.sort((a, b) => {
                const aDiff = Math.min(a.round1, a.round2, a.round3) - percentile;
                const bDiff = Math.min(b.round1, b.round2, b.round3) - percentile;
                return Math.abs(aDiff) - Math.abs(bDiff);
            });

            displayResults(filteredColleges, percentile);
            capInfoSection.classList.remove('hidden');
        }

        // Display Results
        function displayResults(colleges, userPercentile) {
            resultsContainer.innerHTML = '';
            
            if (colleges.length === 0) {
                noResultsDiv.classList.remove('hidden');
                resultsSection.classList.add('hidden');
                return;
            }

            noResultsDiv.classList.add('hidden');
            resultsSection.classList.remove('hidden');

            colleges.forEach(college => {
                const cutoff = Math.min(college.round1, college.round2, college.round3);
                const isSafe = userPercentile >= cutoff + 1;
                const isModerate = userPercentile >= cutoff - 1 && userPercentile < cutoff + 1;
                
                const card = document.createElement('div');
                card.className = `bg-white rounded-lg shadow-md overflow-hidden card-hover ${college.isEligible ? '' : 'opacity-70'}`;
                
                card.innerHTML = `
                    <div class="relative">
                        <img src="${college.image}" alt="${college.alt}" class="w-full h-48 object-cover">
                        ${!college.isEligible ? 
                            `<div class="absolute inset-0 bg-black bg-opacity-40 flex items-center justify-center">
                                <span class="bg-red-500 text-white px-3 py-1 rounded-lg">Not Eligible</span>
                            </div>` : ''}
                        <div class="absolute top-2 right-2 bg-white px-2 py-1 rounded-lg flex items-center">
                            <i class="fas fa-star text-yellow-400 mr-1"></i>
                            <span>${college.rating}</span>
                        </div>
                    </div>
                    <div class="p-6">
                        <div class="flex justify-between items-start mb-2">
                            <h3 class="text-xl font-semibold">${college.name}</h3>
                            <span class="bg-gray-100 text-gray-800 text-xs px-2 py-1 rounded">${college.location}</span>
                        </div>
                        <div class="mb-3">
                            <span class="inline-block bg-blue-100 text-blue-800 px-2 py-1 rounded text-sm">${college.branch}</span>
                        </div>
                        
                        <div class="mb-4">
                            <h4 class="text-sm font-medium text-gray-500 mb-1">CAP Round Cutoffs</h4>
                            <div class="grid grid-cols-3 gap-2">
                                <div class="text-center">
                                    <div class="text-xs text-gray-500">Round 1</div>
                                    <div class="font-medium ${userPercentile >= college.round1 ? 'text-green-600' : 'text-gray-700'}">${college.round1}</div>
                                </div>
                                <div class="text-center">
                                    <div class="text-xs text-gray-500">Round 2</div>
                                    <div class="font-medium ${userPercentile >= college.round2 ? 'text-green-600' : 'text-gray-700'}">${college.round2}</div>
                                </div>
                                <div class="text-center">
                                    <div class="text-xs text-gray-500">Round 3</div>
                                    <div class="font-medium ${userPercentile >= college.round3 ? 'text-green-600' : 'text-gray-700'}">${college.round3}</div>
                                </div>
                            </div>
                        </div>
                        
                        <div class="flex justify-between items-center">
                            <span class="text-gray-700">Fees: ₹${college.fees.toLocaleString('en-IN')}/yr</span>
                            <a href="${college.website}" target="_blank" class="text-blue-600 hover:underline text-sm">Visit Website <i class="fas fa-external-link-alt ml-1 text-xs"></i></a>
                        </div>
                        
                        ${college.isEligible ? `
                        <div class="mt-3">
                            ${isSafe ? 
                                `<div class="bg-green-100 text-green-800 text-sm px-3 py-1 rounded-full inline-flex items-center">
                                    <i class="fas fa-check-circle mr-1"></i> Safe Option
                                </div>` : 
                                isModerate ?
                                `<div class="bg-yellow-100 text-yellow-800 text-sm px-3 py-1 rounded-full inline-flex items-center">
                                    <i class="fas fa-exclamation-circle mr-1"></i> Moderate Chance
                                </div>` :
                                `<div class="bg-blue-100 text-blue-800 text-sm px-3 py-1 rounded-full inline-flex items-center">
                                    <i class="fas fa-info-circle mr-1"></i> Possible in Later Rounds
                                </div>`}
                        </div>
                        ` : ''}
                    </div>
                `;
                
                resultsContainer.appendChild(card);
            });
        }

        // Sort Handler
        function handleSort(e) {
            const sortType = e.target.dataset.sort;
            const currentColleges = Array.from(resultsContainer.querySelectorAll('.bg-white')).map(el => {
                const name = el.querySelector('h3').textContent;
                return collegesData.find(c => c.name === name);
            }).filter(Boolean);
            
            switch(sortType) {
                case 'percentile_high':
                    currentColleges.sort((a, b) => Math.min(b.round1, b.round2, b.round3) - Math.min(a.round1, a.round2, a.round3));
                    break;
                case 'percentile_low':
                    currentColleges.sort((a, b) => Math.min(a.round1, a.round2, a.round3) - Math.min(b.round1, b.round2, b.round3));
                    break;
                case 'name_asc':
                    currentColleges.sort((a, b) => a.name.localeCompare(b.name));
                    break;
                case 'name_desc':
                    currentColleges.sort((a, b) => b.name.localeCompare(a.name));
                    break;
            }
            
            const percentile = parseFloat(document.getElementById('percentile').value);
            displayResults(currentColleges, percentile);
        }
    </script>
</body>
</html>

