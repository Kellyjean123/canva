// Polyfill para compatibilidad
if (!Promise.allSettled) {
    Promise.allSettled = promises =>
        Promise.all(
            promises.map(p =>
                p
                    .then(value => ({ status: "fulfilled", value }))
                    .catch(reason => ({ status: "rejected", reason }))
            )
        );
}

// Verificar si estamos en GitHub Pages
const isGitHubPages = window.location.hostname.includes('github.io');

class PresentationApp {
    constructor() {
        // Configuración base para GitHub Pages
        this.basePath = isGitHubPages ? 
            `/${window.location.pathname.split('/')[1]}` : 
            '';
        
        // Resto del código igual que antes...
    }

    // Modificar métodos que cargan recursos
    async loadTemplates() {
        try {
            const response = await fetch(`${this.basePath}/templates.json`);
            this.templates = await response.json();
            this.renderTemplates();
        } catch (error) {
            console.error("Error loading templates:", error);
            // Cargar templates por defecto
            this.templates = [
                { id: 'default', name: 'Predeterminada', category: 'all', 
                  thumbnail: `${this.basePath}/assets/templates/default.jpg` },
                // ... más templates
            ];
            this.renderTemplates();
        }
    }

    // Modificar URLs de imágenes
    handleImageUpload(event, slideNum) {
        const file = event.target.files[0];
        if (!file) return;

        // Verificar si es GitHub Pages para usar FileReader
        if (isGitHubPages) {
            const reader = new FileReader();
            reader.onload = (e) => {
                this.updateImagePreview(e.target.result, slideNum);
            };
            reader.readAsDataURL(file);
        } else {
            // Lógica normal para otros entornos
        }
    }
}

// Inicialización segura
document.addEventListener('DOMContentLoaded', () => {
    try {
        new PresentationApp();
    } catch (error) {
        console.error("Error initializing app:", error);
        document.body.innerHTML = `
            <div class="error-container">
                <h2>Error al cargar la aplicación</h2>
                <p>Por favor, recarga la página o intenta desde otro dispositivo.</p>
                <button onclick="window.location.reload()">Recargar</button>
            </div>
        `;
    }
});
