<template>
    <div class="galeria-page">
        <!-- Hero Section -->
        <section class="hero-section">
            <div class="hero-background">
                <div class="floating-icons">
                    <div class="floating-icon icon-1">📸</div>
                    <div class="floating-icon icon-2">🎭</div>
                    <div class="floating-icon icon-3">🏆</div>
                    <div class="floating-icon icon-4">🎨</div>
                    <div class="floating-icon icon-5">🎪</div>
                    <div class="floating-icon icon-6">⭐</div>
                </div>
            </div>

            <v-container>
                <div class="hero-content">
                    <div class="hero-badge">
                        <v-icon class="pulse-icon">mdi-camera</v-icon>
                        <span>GALERÍA INSTITUCIONAL</span>
                    </div>

                    <h1 class="hero-title">
                        Momentos
                        <span class="title-highlight">Memorables</span>
                    </h1>

                    <p class="hero-description">
                        Revive los mejores momentos de nuestra comunidad educativa.
                        Desde eventos especiales hasta actividades cotidianas que hacen
                        de nuestra institución un lugar único.
                    </p>

                    <div class="stats-container">
                        <div class="stat-item">
                            <div class="stat-number">{{ totalImages }}</div>
                            <div class="stat-label">Fotografías</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">{{ categories.length }}</div>
                            <div class="stat-label">Categorías</div>
                        </div>
                        <div class="stat-item">
                            <div class="stat-number">{{ totalEvents }}</div>
                            <div class="stat-label">Eventos</div>
                        </div>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Filter Section -->
        <section class="filter-section">
            <v-container>
                <div class="filter-content">
                    <h3 class="filter-title">Explora por Categoría</h3>
                    <div class="filter-tabs">
                        <v-chip-group v-model="selectedCategory" mandatory color="green">
                            <v-chip v-for="category in categories" :key="category.id" :value="category.id"
                                :prepend-icon="category.icon" size="large" class="filter-chip">
                                {{ category.name }}
                                <v-badge v-if="category.count" :content="category.count" color="white"
                                    text-color="green" class="ml-2" />
                            </v-chip>
                        </v-chip-group>
                    </div>
                </div>
            </v-container>
        </section>

        <!-- Gallery Section -->
        <section class="gallery-section">
            <v-container>
                <div class="gallery-grid">
                    <div v-for="(image, index) in filteredImages" :key="image.id" class="gallery-item"
                        :class="`item-${(index % 4) + 1}`" @click="openDialog(image, index)">

                        <v-card class="gallery-card" elevation="4" hover>
                            <div class="image-container">
                                <v-img :src="image.src" :alt="image.title" aspect-ratio="1" cover class="gallery-image">
                                    <template v-slot:placeholder>
                                        <div class="image-placeholder">
                                            <v-icon size="64" color="grey-lighten-2">mdi-image-outline</v-icon>
                                        </div>
                                    </template>
                                </v-img>

                                <div class="image-overlay">
                                    <div class="overlay-content">
                                        <v-icon size="48" color="white" class="zoom-icon">mdi-magnify-plus</v-icon>
                                        <p class="overlay-text">Ver detalles</p>
                                    </div>
                                </div>

                                <div class="image-category">
                                    <v-chip size="small" :color="getCategoryColor(image.category)">
                                        {{ image.category }}
                                    </v-chip>
                                </div>
                            </div>

                            <v-card-text class="image-info">
                                <h4 class="image-title">{{ image.title }}</h4>
                                <p class="image-description">{{ image.description }}</p>
                                <div class="image-meta">
                                    <span class="image-date">
                                        <v-icon size="small">mdi-calendar</v-icon>
                                        {{ formatDate(image.date) }}
                                    </span>
                                    <span class="image-location" v-if="image.location">
                                        <v-icon size="small">mdi-map-marker</v-icon>
                                        {{ image.location }}
                                    </span>
                                </div>
                            </v-card-text>
                        </v-card>
                    </div>
                </div>

                <!-- Load More Button -->
                <div class="load-more-section" v-if="hasMoreImages">
                    <v-btn size="large" variant="outlined" color="green" prepend-icon="mdi-plus" @click="loadMoreImages"
                        :loading="loadingMore" class="load-more-btn">
                        Cargar más imágenes
                    </v-btn>
                </div>
            </v-container>
        </section>

        <!-- Featured Events -->
        <section class="featured-section">
            <v-container>
                <div class="section-header">
                    <v-icon class="section-icon">mdi-star</v-icon>
                    <h2 class="section-title">Eventos Destacados</h2>
                    <p class="section-description">
                        Los momentos más especiales de nuestra comunidad
                    </p>
                </div>

                <div class="featured-grid">
                    <v-card v-for="event in featuredEvents" :key="event.id" class="featured-card" elevation="8"
                        @click="showEventGallery(event)">

                        <div class="featured-header" :style="{ background: event.gradient }">
                            <div class="featured-icon">{{ event.icon }}</div>
                            <div class="featured-badge">{{ event.badge }}</div>
                        </div>

                        <v-card-text class="featured-content">
                            <h3 class="featured-title">{{ event.title }}</h3>
                            <p class="featured-description">{{ event.description }}</p>

                            <div class="featured-stats">
                                <div class="stat">
                                    <v-icon size="small">mdi-camera</v-icon>
                                    <span>{{ event.imageCount }} fotos</span>
                                </div>
                                <div class="stat">
                                    <v-icon size="small">mdi-calendar</v-icon>
                                    <span>{{ event.date }}</span>
                                </div>
                            </div>

                            <div class="featured-preview">
                                <div v-for="preview in event.preview" :key="preview" class="preview-image">
                                    <v-img :src="preview" aspect-ratio="1" cover />
                                </div>
                            </div>
                        </v-card-text>
                    </v-card>
                </div>
            </v-container>
        </section>

        <!-- Image Dialog -->
        <v-dialog v-model="imageDialog" max-width="1200px">
            <v-card v-if="selectedImage" class="dialog-card">
                <v-card-title class="dialog-header">
                    <span class="dialog-title">{{ selectedImage.title }}</span>
                    <v-spacer></v-spacer>
                    <v-btn icon variant="text" @click="imageDialog = false">
                        <v-icon>mdi-close</v-icon>
                    </v-btn>
                </v-card-title>

                <div class="dialog-content">
                    <div class="dialog-image">
                        <v-img :src="selectedImage.src" :alt="selectedImage.title" contain />

                        <div class="dialog-navigation">
                            <v-btn icon size="large" variant="elevated" color="white" @click="previousImage"
                                :disabled="currentImageIndex === 0" class="nav-btn nav-prev">
                                <v-icon>mdi-chevron-left</v-icon>
                            </v-btn>

                            <v-btn icon size="large" variant="elevated" color="white" @click="nextImage"
                                :disabled="currentImageIndex === filteredImages.length - 1" class="nav-btn nav-next">
                                <v-icon>mdi-chevron-right</v-icon>
                            </v-btn>
                        </div>
                    </div>

                    <div class="dialog-info">
                        <div class="dialog-meta">
                            <v-chip :color="getCategoryColor(selectedImage.category)" class="mb-3">
                                {{ selectedImage.category }}
                            </v-chip>

                            <h3 class="dialog-image-title">{{ selectedImage.title }}</h3>
                            <p class="dialog-description">{{ selectedImage.description }}</p>

                            <div class="dialog-details">
                                <div class="detail-item">
                                    <v-icon>mdi-calendar</v-icon>
                                    <span>{{ formatDate(selectedImage.date) }}</span>
                                </div>
                                <div class="detail-item" v-if="selectedImage.location">
                                    <v-icon>mdi-map-marker</v-icon>
                                    <span>{{ selectedImage.location }}</span>
                                </div>
                                <div class="detail-item" v-if="selectedImage.photographer">
                                    <v-icon>mdi-camera</v-icon>
                                    <span>{{ selectedImage.photographer }}</span>
                                </div>
                            </div>
                        </div>

                        <div class="dialog-actions">
                            <v-btn variant="outlined" color="green" prepend-icon="mdi-download">
                                Descargar
                            </v-btn>
                            <v-btn variant="outlined" color="blue" prepend-icon="mdi-share">
                                Compartir
                            </v-btn>
                        </div>
                    </div>
                </div>
            </v-card>
        </v-dialog>
    </div>
</template>

<script>
export default {
    name: "GaleriaPage",

    data() {
        return {
            selectedCategory: 'todas',
            imageDialog: false,
            selectedImage: null,
            currentImageIndex: 0,
            loadingMore: false,
            displayedImages: 12,

            categories: [
                { id: 'todas', name: 'Todas', icon: 'mdi-view-grid', count: null },
                { id: 'eventos', name: 'Eventos Especiales', icon: 'mdi-calendar-star', count: 1 },
                { id: 'academico', name: 'Vida Académica', icon: 'mdi-school', count: 2 },
                { id: 'deportes', name: 'Deportes', icon: 'mdi-soccer', count: 1 },
                { id: 'cultura', name: 'Actividades Culturales', icon: 'mdi-music', count: 2 },
                { id: 'graduacion', name: 'Graduaciones', icon: 'mdi-account-school', count: 1 }
            ],

            images: [
                {
                    id: 1,
                    title: "Lanzamiento de promoción 2025",
                    description: "Estudiantes de grado 11 celebrando el lanzamiento de la promoción 2025.",
                    src: "/img/lanzamientopromocion.png",
                    category: "Eventos Especiales",
                    date: "2025-03-15",
                    location: "Polideportivo Institucional",
                    photographer: "Club de Fotografía"
                },
                {
                    id: 3,
                    title: "Taller de expresión oral",
                    description: "Aprender a hablar es aprender a conectar. Así vivimos nuestro taller de expresión oral. 🎙️💬❤️",
                    src: "/img/talleroral.png",
                    category: "Vida Académica",
                    date: "2025-03-24",
                    location: "Biblioteca Escolar",
                },
                {
                    id: 4,
                    title: "Torneo de microfútbol",
                    description: "Enfrentamiento entre los equipos de microfútbol del colegio, un evento lleno de emoción y compañerismo.",
                    src: "/img/futbol.png",
                    category: "Deportes",
                    date: "2025-03-20",
                    location: "Polideportivo Institucional",
                },
                {
                    id: 5,
                    title: "Concierto de Navidad",
                    description: "Presentación del coro institucional durante las celebraciones navideñas.",
                    src: "https://images.unsplash.com/photo-1493225457124-a3eb161ffa5f?w=800&h=600&fit=crop",
                    category: "Actividades Culturales",
                    date: "2023-12-15",
                    location: "Capilla Institucional"
                },
                {
                    id: 6,
                    title: "Graduación Bachilleres 2023",
                    description: "Ceremonia de graduación de la promoción 2023, un momento lleno de orgullo y esperanza.",
                    src: "/img/graduacion.png",
                    category: "Graduaciones",
                    date: "2023-12-08",
                    location: "Ademacor"
                },
                {
                    id: 7,
                    title: "Taller de Periodismo",
                    description: "Estudiantes aprendiendo técnicas de periodismo radiofónico con profesionales del medio.",
                    src: "https://images.unsplash.com/photo-1504711434969-e33886168f5c?w=800&h=600&fit=crop",
                    category: "Radio Escolar",
                    date: "2024-01-18",
                    location: "Aula de Medios"
                },
                {
                    id: 8,
                    title: "Día del libro",
                    description: "En el marco del Día del Libro, celebramos la lectura con la actividad café literario, donde los estudiantes compartieron sus libros favoritos y disfrutaron de un ambiente de lectura.",
                    src: "/img/cafeliterario.png",
                    category: "Actividades Culturales",
                    date: "2025-04-23",
                    location: "Plaza Central"
                },
                {
                    id: 9,
                    title: "Taller de lettering",
                    description: "El proyecto Voces avanza a pasos de gigante. Hoy, taller de Lettering para los 20 estudiantes beneficiados. ",
                    src: "/img/tallerlettering.png",
                    category: "Vida Académica",
                    date: "2024-02-18",
                    location: "Biblioteca Escolar",
                },
                {
                    id: 10,
                    title: "Reunion con el Alcalde",
                    description: "En el Coliseo Miguel Happy Lora, el Alcalde inspiró a toda la promo 2025 de Montería, con su mensaje sobre la importancia de la preparación para las pruebas que vienen.",
                    src: "/img/reunionalcalde.png",
                    category: "Radio Escolar",
                    date: "2025-02-15",
                    location: "Coliseo Miguel Happy Lora",
                }
            ],

            featuredEvents: [
                {
                    id: 1,
                    title: "Lanzamiento de promoción 2025",
                    description: "El evento más esperado del año donde nuestros estudiantes brillan con luz propia",
                    icon: "🌟",
                    badge: "ANUAL",
                    date: "Marzo 2025",
                    imageCount: 45,
                    gradient: "linear-gradient(135deg, #667eea 0%, #764ba2 100%)",
                    preview: [
                        "/img/lanzamientopromocion.png",
                        "/img/lanzamientopromocion2.png",
                        "/img/lanzamientopromocion3.png"
                    ]
                },
                {
                    id: 2,
                    title: "Torneo de Microfútbol",
                    description: "Evento deportivo que reúne a los mejores equipos del colegio en una competencia emocionante",
                    icon: "⚽",
                    badge: "ESPECIAL",
                    date: "Mayo 2025",
                    imageCount: 32,
                    gradient: "linear-gradient(135deg, #f093fb 0%, #f5576c 100%)",
                    preview: [
                        "img/futbol.png",
                        "img/futbol2.png",
                        "img/futbol3.png"
                    ]
                },
                {
                    id: 3,
                    title: "Graduación 2023",
                    description: "El momento más emotivo: despedir a nuestros bachilleres con orgullo",
                    icon: "🎓",
                    badge: "MEMORABLE",
                    date: "Diciembre 2023",
                    imageCount: 28,
                    gradient: "linear-gradient(135deg, #4facfe 0%, #00f2fe 100%)",
                    preview: [
                        "/img/graduacion.png",
                        "/img/graduacion2.png",
                        "/img/graduacion3.png"
                    ]
                }
            ]
        };
    },

    computed: {
        filteredImages() {
            if (this.selectedCategory === 'todas') {
                return this.images.slice(0, this.displayedImages);
            }

            const categoryName = this.categories.find(cat => cat.id === this.selectedCategory)?.name;
            return this.images
                .filter(image => image.category === categoryName)
                .slice(0, this.displayedImages);
        },

        totalImages() {
            return this.images.length;
        },

        totalEvents() {
            return this.featuredEvents.length;
        },

        hasMoreImages() {
            const totalAvailable = this.selectedCategory === 'todas'
                ? this.images.length
                : this.images.filter(image => {
                    const categoryName = this.categories.find(cat => cat.id === this.selectedCategory)?.name;
                    return image.category === categoryName;
                }).length;

            return this.displayedImages < totalAvailable;
        }
    },

    methods: {
        openDialog(image, index) {
            this.selectedImage = image;
            this.currentImageIndex = index;
            this.imageDialog = true;
        },

        previousImage() {
            if (this.currentImageIndex > 0) {
                this.currentImageIndex--;
                this.selectedImage = this.filteredImages[this.currentImageIndex];
            }
        },

        nextImage() {
            if (this.currentImageIndex < this.filteredImages.length - 1) {
                this.currentImageIndex++;
                this.selectedImage = this.filteredImages[this.currentImageIndex];
            }
        },

        loadMoreImages() {
            this.loadingMore = true;

            setTimeout(() => {
                this.displayedImages += 8;
                this.loadingMore = false;
            }, 1000);
        },

        getCategoryColor(category) {
            const colorMap = {
                'Eventos Especiales': 'purple',
                'Radio Escolar': 'green',
                'Vida Académica': 'blue',
                'Deportes': 'orange',
                'Actividades Culturales': 'pink',
                'Graduaciones': 'teal'
            };
            return colorMap[category] || 'grey';
        },

        formatDate(dateString) {
            const date = new Date(dateString);
            return date.toLocaleDateString('es-ES', {
                year: 'numeric',
                month: 'long',
                day: 'numeric'
            });
        },

        showEventGallery(event) {
            // Implementar navegación a galería específica del evento
            console.log('Mostrar galería del evento:', event.title);
        }
    }
};
</script>

<style scoped>
.galeria-page {
    min-height: 100vh;
    background: linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%);
}

/* Hero Section */
.hero-section {
    position: relative;
    padding: 80px 0;
    background: linear-gradient(135deg, #1b5e20 0%, #2e7d32 50%, #1b5e20 100%);
    color: white;
    overflow: hidden;
}

.hero-background {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    opacity: 0.1;
}

.floating-icons {
    position: absolute;
    width: 100%;
    height: 100%;
}

.floating-icon {
    position: absolute;
    font-size: 3rem;
    animation: float 6s ease-in-out infinite;
}

.icon-1 { top: 20%; left: 10%; animation-delay: 0s; }
.icon-2 { top: 30%; right: 15%; animation-delay: 1s; }
.icon-3 { bottom: 40%; left: 20%; animation-delay: 2s; }
.icon-4 { top: 60%; right: 25%; animation-delay: 3s; }
.icon-5 { bottom: 20%; right: 10%; animation-delay: 4s; }
.icon-6 { top: 70%; left: 30%; animation-delay: 5s; }

@keyframes float {
    0%, 100% { transform: translateY(0px) rotate(0deg); }
    25% { transform: translateY(-20px) rotate(5deg); }
    50% { transform: translateY(-10px) rotate(-5deg); }
    75% { transform: translateY(-15px) rotate(3deg); }
}

.hero-content {
    position: relative;
    z-index: 2;
    text-align: center;
    max-width: 800px;
    margin: 0 auto;
}

.hero-badge {
    display: inline-flex;
    align-items: center;
    gap: 10px;
    background: rgba(255, 255, 255, 0.1);
    padding: 8px 20px;
    border-radius: 25px;
    margin-bottom: 20px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.pulse-icon {
    animation: pulse 1.5s ease-in-out infinite;
    color: #4caf50;
}

@keyframes pulse {
    0%, 100% { opacity: 1; transform: scale(1); }
    50% { opacity: 0.7; transform: scale(1.1); }
}

.hero-title {
    font-size: 3.5rem;
    font-weight: 800;
    margin-bottom: 20px;
    line-height: 1.1;
}

.title-highlight {
    background: linear-gradient(45deg, #81c784, #c8e6c9);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.hero-description {
    font-size: 1.2rem;
    opacity: 0.9;
    margin-bottom: 40px;
    line-height: 1.6;
}

.stats-container {
    display: flex;
    justify-content: center;
    gap: 40px;
    flex-wrap: wrap;
}

.stat-item {
    text-align: center;
}

.stat-number {
    font-size: 2.5rem;
    font-weight: 700;
    color: #81c784;
    margin-bottom: 5px;
}

.stat-label {
    font-size: 1rem;
    opacity: 0.8;
    text-transform: uppercase;
    letter-spacing: 1px;
}

/* Filter Section */
.filter-section {
    padding: 40px 0;
    background: white;
    box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.filter-content {
    text-align: center;
}

.filter-title {
    font-size: 1.8rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 30px;
}

.filter-tabs {
    display: flex;
    justify-content: center;
}

.filter-chip {
    margin: 0 5px;
    font-weight: 600;
}

/* Gallery Section */
.gallery-section {
    padding: 60px 0;
}

.gallery-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 25px;
    margin-bottom: 40px;
}

.gallery-item {
    transition: transform 0.3s ease;
}

.gallery-card {
    border-radius: 16px;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.3s ease;
}

.gallery-card:hover {
    transform: translateY(-8px);
    box-shadow: 0 20px 40px rgba(0,0,0,0.15);
}

.image-container {
    position: relative;
    overflow: hidden;
}

.gallery-image {
    transition: transform 0.3s ease;
}

.gallery-card:hover .gallery-image {
    transform: scale(1.05);
}

.image-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0,0,0,0.6);
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
}

.gallery-card:hover .image-overlay {
    opacity: 1;
}

.overlay-content {
    text-align: center;
    color: white;
}

.zoom-icon {
    margin-bottom: 10px;
    animation: bounce 1s ease-in-out infinite;
}

@keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(-10px); }
}

.overlay-text {
    font-weight: 600;
    font-size: 1.1rem;
    margin: 0;
}

.image-category {
    position: absolute;
    top: 12px;
    left: 12px;
    z-index: 1;
}

.image-placeholder {
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #f5f5f5;
}

.image-info {
    padding: 20px;
}

.image-title {
    font-size: 1.2rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 8px;
    line-height: 1.3;
}

.image-description {
    color: #666;
    font-size: 0.95rem;
    line-height: 1.4;
    margin-bottom: 15px;
}

.image-meta {
    display: flex;
    align-items: center;
    gap: 15px;
    flex-wrap: wrap;
}

.image-date,
.image-location {
    display: flex;
    align-items: center;
    gap: 5px;
    font-size: 0.85rem;
    color: #888;
}

/* Load More Section */
.load-more-section {
    text-align: center;
    margin-top: 40px;
}

.load-more-btn {
    padding: 15px 30px;
    font-weight: 600;
    border-radius: 25px;
    text-transform: none;
}

/* Featured Section */
.featured-section {
    padding: 80px 0;
    background: linear-gradient(135deg, #f8f9fa 0%, #e9ecef 100%);
}

.section-header {
    text-align: center;
    margin-bottom: 50px;
}

.section-icon {
    font-size: 3rem;
    color: #2e7d32;
    margin-bottom: 15px;
}

.section-title {
    font-size: 2.5rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 15px;
}

.section-description {
    font-size: 1.2rem;
    color: #666;
    max-width: 600px;
    margin: 0 auto;
}

.featured-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(350px, 1fr));
    gap: 30px;
}

.featured-card {
    border-radius: 20px;
    overflow: hidden;
    cursor: pointer;
    transition: all 0.3s ease;
    background: white;
}

.featured-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 25px 50px rgba(0,0,0,0.15);
}

.featured-header {
    position: relative;
    padding: 30px 25px;
    display: flex;
    align-items: center;
    justify-content: space-between;
    color: white;
}

.featured-icon {
    font-size: 2.5rem;
}

.featured-badge {
    background: rgba(255,255,255,0.2);
    padding: 8px 15px;
    border-radius: 20px;
    font-size: 0.8rem;
    font-weight: 700;
    letter-spacing: 1px;
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255,255,255,0.3);
}

.featured-content {
    padding: 25px;
}

.featured-title {
    font-size: 1.4rem;
    font-weight: 700;
    color: #1b5e20;
    margin-bottom: 12px;
}

.featured-description {
    color: #666;
    line-height: 1.5;
    margin-bottom: 20px;
}

.featured-stats {
    display: flex;
    gap: 20px;
    margin-bottom: 20px;
}

.stat {
    display: flex;
    align-items: center;
    gap: 6px;
    font-size: 0.9rem;
    color: #888;
}

.featured-preview {
    display: flex;
    gap: 8px;
}

.preview-image {
    width: 50px;
    height: 50px;
    border-radius: 10px;
    overflow: hidden;
    opacity: 0.8;
    transition: opacity 0.3s ease;
}

.featured-card:hover .preview-image {
    opacity: 1;
}

/* Dialog Styles */
.dialog-card {
    border-radius: 16px;
    overflow: hidden;
}

.dialog-header {
    background: #1b5e20;
    color: white;
    padding: 20px 25px;
}

.dialog-title {
    font-size: 1.3rem;
    font-weight: 600;
}

.dialog-content {
    display: grid;
    grid-template-columns: 2fr 1fr;
    min-height: 500px;
}

.dialog-image {
    position: relative;
    background: #f5f5f5;
}

.dialog-navigation {
    position: absolute;
    top: 50%;
    left: 0;
    right: 0;
    transform: translateY(-50%);
    display: flex;
    justify-content: space-between;
    padding: 0 20px;
    z-index: 2;
}

.nav-btn {
    box-shadow: 0 4px 12px rgba(0,0,0,0.15);
    transition: all 0.3s ease;
}

.nav-btn:hover {
    transform: scale(1.1);
    box-shadow: 0 6px 20px rgba(0,0,0,0.2);
}

.dialog-info {
    padding: 25px;
    display: flex;
    flex-direction: column;
    background: #fafafa;
}

.dialog-meta {
    flex: 1;
}

.dialog-image-title {
    font-size: 1.3rem;
    font-weight: 600;
    color: #1b5e20;
    margin-bottom: 12px;
    line-height: 1.3;
}

.dialog-description {
    color: #666;
    line-height: 1.5;
    margin-bottom: 25px;
}

.dialog-details {
    margin-bottom: 30px;
}

.detail-item {
    display: flex;
    align-items: center;
    gap: 10px;
    margin-bottom: 12px;
    color: #555;
    font-size: 0.95rem;
}

.dialog-actions {
    display: flex;
    gap: 12px;
}

/* Responsive Design */
@media (max-width: 1200px) {
    .dialog-content {
        grid-template-columns: 1fr;
    }

    .dialog-image {
        min-height: 400px;
    }
}

@media (max-width: 768px) {
    .hero-title {
        font-size: 2.5rem;
    }

    .hero-description {
        font-size: 1rem;
    }

    .stats-container {
        gap: 20px;
    }

    .stat-number {
        font-size: 2rem;
    }

    .gallery-grid {
        grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
        gap: 20px;
    }

    .featured-grid {
        grid-template-columns: 1fr;
    }

    .filter-tabs {
        overflow-x: auto;
        padding: 0 10px;
    }

    .section-title {
        font-size: 2rem;
    }

    .floating-icons {
        display: none;
    }
}

@media (max-width: 480px) {
    .hero-section {
        padding: 60px 0;
    }

    .hero-title {
        font-size: 2rem;
    }

    .stats-container {
        flex-direction: column;
        gap: 15px;
    }

    .gallery-grid {
        grid-template-columns: 1fr;
        gap: 15px;
    }

    .image-meta {
        flex-direction: column;
        align-items: flex-start;
        gap: 8px;
    }

    .dialog-navigation {
        padding: 0 10px;
    }

    .nav-btn {
        width: 40px;
        height: 40px;
    }
}

/* Animation Classes */
.fade-enter-active,
.fade-leave-active {
    transition: opacity 0.3s ease;
}

.fade-enter-from,
.fade-leave-to {
    opacity: 0;
}

.slide-up-enter-active,
.slide-up-leave-active {
    transition: all 0.3s ease;
}

.slide-up-enter-from {
    opacity: 0;
    transform: translateY(30px);
}

.slide-up-leave-to {
    opacity: 0;
    transform: translateY(-30px);
}

/* Custom Scrollbar */
::-webkit-scrollbar {
    width: 8px;
}

::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 4px;
}

::-webkit-scrollbar-thumb {
    background: #2e7d32;
    border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
    background: #1b5e20;
}

/* Loading Animation */
@keyframes shimmer {
    0% {
        background-position: -468px 0;
    }
    100% {
        background-position: 468px 0;
    }
}

.loading-shimmer {
    animation: shimmer 1.5s ease-in-out infinite;
    background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
    background-size: 1000px 100%;
}

/* Focus States for Accessibility */
.gallery-card:focus,
.featured-card:focus,
.filter-chip:focus {
    outline: 2px solid #2e7d32;
    outline-offset: 2px;
}

/* High Contrast Mode Support */
@media (prefers-contrast: high) {
    .hero-section {
        background: #000;
        color: #fff;
    }

    .image-overlay {
        background: rgba(0,0,0,0.8);
    }

    .gallery-card {
        border: 2px solid #333;
    }
}

/* Reduced Motion Support */
@media (prefers-reduced-motion: reduce) {
    .floating-icon,
    .pulse-icon,
    .zoom-icon {
        animation: none;
    }

    .gallery-card,
    .featured-card,
    .nav-btn {
        transition: none;
    }
}

/* Print Styles */
@media print {
    .hero-section,
    .filter-section,
    .dialog-navigation,
    .dialog-actions {
        display: none;
    }

    .gallery-grid {
        grid-template-columns: repeat(2, 1fr);
        gap: 15px;
    }

    .gallery-card {
        break-inside: avoid;
        box-shadow: none;
        border: 1px solid #ddd;
    }
}

/* Additional Utility Classes */
.text-gradient {
    background: linear-gradient(45deg, #2e7d32, #81c784);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
}

.glass-effect {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.2);
}

.shadow-custom {
    box-shadow: 0 10px 30px rgba(0, 0, 0, 0.1);
}

.border-radius-custom {
    border-radius: 16px;
}

/* Grid Layout Variations */
.gallery-grid.masonry {
    column-count: 3;
    column-gap: 25px;
}

.gallery-grid.masonry .gallery-item {
    display: inline-block;
    margin-bottom: 25px;
    width: 100%;
}

@media (max-width: 768px) {
    .gallery-grid.masonry {
        column-count: 2;
    }
}

@media (max-width: 480px) {
    .gallery-grid.masonry {
        column-count: 1;
    }
}

/* Loading States */
.gallery-item.loading {
    opacity: 0.5;
    pointer-events: none;
}

.gallery-item.loading .gallery-image {
    background: linear-gradient(90deg, #f0f0f0 25%, #e0e0e0 50%, #f0f0f0 75%);
    background-size: 200% 100%;
    animation: shimmer 1.5s ease-in-out infinite;
}

/* Error States */
.gallery-item.error .gallery-image {
    background: #f5f5f5;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #999;
    font-size: 0.9rem;
}

.gallery-item.error .gallery-image::before {
    content: "Error al cargar imagen";
}

/* Hover Effects for Touch Devices */
@media (hover: none) {
    .gallery-card:hover {
        transform: none;
        box-shadow: 0 4px 12px rgba(0,0,0,0.1);
    }

    .image-overlay {
        opacity: 0;
    }

    .gallery-card:active .image-overlay {
        opacity: 1;
    }
}
    </style>