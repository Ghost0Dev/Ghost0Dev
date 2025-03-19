Hi 👋! My name is Ghost0Dev and I'm a developer from Germany 🇩🇪

Timezone: GMT+1

import { useEffect, useState } from "react";
import { Card, CardContent } from "@/components/ui/card";
import { Button } from "@/components/ui/button";
import { motion } from "framer-motion";
import { Globe } from "lucide-react";

const GITHUB_API_URL = "https://api.github.com/repos/Ghost0Dev";

export default function GitHubRepoWidget() {
  const [repo, setRepo] = useState(null);
  const [languages, setLanguages] = useState({});

  useEffect(() => {
    fetch(`${GITHUB_API_URL}`)
      .then((res) => res.json())
      .then((data) => setRepo(data));

    fetch(`${GITHUB_API_URL}/languages`)
      .then((res) => res.json())
      .then((data) => setLanguages(data));
  }, []);

  return (
    <motion.div
      initial={{ opacity: 0, scale: 0.9 }}
      animate={{ opacity: 1, scale: 1 }}
      transition={{ duration: 0.5 }}
      className="flex justify-center mt-10"
    >
      <Card className="rounded-2xl shadow-lg p-4 w-80 bg-gray-900 text-white">
        <CardContent>
          {repo ? (
            <div>
              <h2 className="text-xl font-bold mb-2">{repo.name}</h2>
              <p className="text-sm text-gray-400 mb-4">{repo.description}</p>
              <div className="mb-4">
                {Object.keys(languages).map((lang) => (
                  <span key={lang} className="mr-2 text-sm bg-gray-700 px-2 py-1 rounded">
                    {lang}
                  </span>
                ))}
              </div>
              <Button asChild className="w-full">
                <a href={repo.html_url} target="_blank" rel="noopener noreferrer">
                  <Globe className="mr-2" size={16} /> GitHub öffnen
                </a>
              </Button>
            </div>
          ) : (
            <p className="text-center">Lade Daten...</p>
          )}
        </CardContent>
      </Card>
    </motion.div>
  );
}






