import React, { useState, useEffect, useRef } from 'react';
import { 
  Sparkles, 
  Upload, 
  Link2, 
  ChevronRight, 
  FileText, 
  FileCode, 
  Trash2, 
  Copy, 
  Check, 
  Download, 
  RefreshCw, 
  Layers, 
  HelpCircle, 
  Eye, 
  AlertCircle,
  FileDown,
  ExternalLink,
  Flame,
  ShieldCheck,
  Zap,
  CheckCircle2,
  Info
} from 'lucide-react';

// Dynamic loader for mammoth.js (DOCX extraction) and jsPDF (PDF download)
const loadExternalLibraries = () => {
  return new Promise((resolve) => {
    let mammothLoaded = !!window.mammoth;
    let jspdfLoaded = !!window.jspdf;

    const checkAndResolve = () => {
      if (window.mammoth && window.jspdf) {
        resolve(true);
      }
    };

    if (mammothLoaded && jspdfLoaded) {
      resolve(true);
      return;
    }

    if (!window.mammoth) {
      const mammothScript = document.createElement('script');
      mammothScript.src = "https://cdnjs.cloudflare.com/ajax/libs/mammoth/1.4.21/mammoth.browser.min.js";
      mammothScript.onload = () => {
        mammothLoaded = true;
        checkAndResolve();
      };
      document.head.appendChild(mammothScript);
    }

    if (!window.jspdf) {
      const jspdfScript = document.createElement('script');
      jspdfScript.src = "https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js";
      jspdfScript.onload = () => {
        jspdfLoaded = true;
        checkAndResolve();
      };
      document.head.appendChild(jspdfScript);
    }
  });
};

export default function App() {
  // App view states: 'input' or 'result'
  const [viewState, setViewState] = useState('input');
  
  // Library load status
  const [libsReady, setLibsReady] = useState(false);

  // Form Field States
  const [clientName, setClientName] = useState('');
  const [product, setProduct] = useState('Hot Tub'); // Hot Tub, Swim Spa, Both
  const [category, setCategory] = useState('Evergreen'); // Evergreen, Holiday, Events, Custom
  const [holidayName, setHolidayName] = useState('');
  const [customAngle, setCustomAngle] = useState('');
  const [referenceText, setReferenceText] = useState('');
  const [urls, setUrls] = useState('');
  const [additionalInstructions, setAdditionalInstructions] = useState('');
  const [uploadedFiles, setUploadedFiles] = useState([]);
  
  // System/API state
  const [isGenerating, setIsGenerating] = useState(false);
  const [generationStep, setGenerationStep] = useState('');
  const [apiError, setApiError] = useState(null);
  const [successToast, setSuccessToast] = useState('');

  // Generated copy state
  const [generatedCopy, setGeneratedCopy] = useState({
    hero: {
      headline: "Escape the Noise: Premium Hydrotherapy Awaits You at [CLIENT NAME]",
      subheadline: "Transform your backyard into a private wellness sanctuary. Lock in exclusive showroom savings and book your private wet-test consultation today.",
      cta: "Claim Your Showroom Pass"
    },
    problem: "Modern life is fast, noisy, and physically demanding. Chronic muscle tension, restless nights, and the constant hum of stress shouldn't be your 'normal'. Yet, finding genuine, distraction-free time to unwind with the people who matter most feels nearly impossible.",
    solution: "The Ultimate Wellness Oasis: Handcrafted hot tubs and swim spas engineered for targeted pain relief and pure mental decompression. Discover industry-leading water purification, ergonomic seating designed by therapeutic specialists, and unmatched energy-efficiency built to perform through harsh winters.",
    benefits: [
      "Targeted Hydrotherapy: Precision jets engineered to relieve pressure points, improve blood circulation, and alleviate persistent lower-back stiffness.",
      "Pure Recovery Sleep: 15 minutes of evening warm-water immersion naturally drops core temperature, guiding you into deeper, restorative sleep cycles.",
      "Interruption-Free Connection: Create a sanctuary where screens are replaced with real conversation, reconnecting your family with distraction-free quality time."
    ],
    trust: "Backed by over 20 years of local showroom expertise, factory-certified installation teams, and a comprehensive lifetime shell warranty. Plus, take advantage of special 0% APR financing options to bring everyday luxury home with confidence.",
    objections: [
      {
        question: "Isn't the ongoing maintenance and water upkeep a daily hassle?",
        answer: "Not anymore. Our advanced automated filtration and eco-friendly UV sanitization systems do the heavy lifting, reducing chemicals by up to 75% and requiring only minutes of weekly attention."
      },
      {
        question: "How much will this impact my monthly electrical bill?",
        answer: "Surprisingly little. Thanks to our full-foam high-density insulation and custom-fit locking thermal covers, our units operate efficiently for as low as the price of a daily cup of coffee."
      },
      {
        question: "How do I know which model is right for my space and budget?",
        answer: "We make it stress-free. Book a private showroom consultation to explore layouts side-by-side, take advantage of our virtual 3D yard-planner, and even enjoy a private 'wet test' in a secluded space."
      }
    ],
    urgency: "Exclusive showroom incentive allocations are strictly limited. Secure your priority savings voucher and guarantee installation before our current inventory sells out.",
    finalCta: {
      headline: "Ready to Experience Ultimate Daily Decompression?",
      cta: "Book Your Showroom Consultation"
    }
  });

  // Track Copy feedback per block
  const [copiedBlock, setCopiedBlock] = useState(null);

  // Initialize external scripts on load
  useEffect(() => {
    loadExternalLibraries().then(() => {
      setLibsReady(true);
    });
  }, []);

  // Show dynamic self-clearing toast
  const triggerToast = (msg) => {
    setSuccessToast(msg);
    setTimeout(() => {
      setSuccessToast('');
    }, 3500);
  };

  const handleFileUpload = async (e) => {
    const files = Array.from(e.target.files);
    if (!files.length) return;

    for (const file of files) {
      const fileObj = {
        name: file.name,
        type: file.type,
        size: (file.size / 1024).toFixed(1) + ' KB',
        content: null,
        base64: null,
        isPDF: file.type === 'application/pdf'
      };

      try {
        if (file.type === 'text/plain') {
          // Read TXT files directly
          const text = await readFileAsText(file);
          fileObj.content = text;
          setUploadedFiles(prev => [...prev, fileObj]);
        } else if (file.type === 'application/pdf') {
          // Convert PDF to Base64 for native inline transfer to Gemini
          const base64 = await readFileAsDataURL(file);
          const cleanBase64 = base64.split(',')[1];
          fileObj.base64 = cleanBase64;
          setUploadedFiles(prev => [...prev, fileObj]);
        } else if (file.name.endsWith('.docx')) {
          // Extract DOCX using client-side mammoth
          if (!window.mammoth) {
            triggerToast("Docx parser is still loading... Please wait a second.");
            continue;
          }
          const arrayBuffer = await readFileAsArrayBuffer(file);
          const result = await window.mammoth.extractRawText({ arrayBuffer });
          fileObj.content = result.value;
          setUploadedFiles(prev => [...prev, fileObj]);
        } else {
          // Fallback to text reading for unsupported text extensions
          const text = await readFileAsText(file);
          fileObj.content = text;
          setUploadedFiles(prev => [...prev, fileObj]);
        }
        triggerToast(`Uploaded and parsed: ${file.name}`);
      } catch (err) {
        console.error("Error reading file:", err);
        triggerToast(`Failed to parse file: ${file.name}`);
      }
    }
    // Reset file input target value to allow re-uploads
    e.target.value = '';
  };

  const readFileAsText = (file) => {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = () => resolve(reader.result);
      reader.onerror = () => reject(reader.error);
      reader.readAsText(file);
    });
  };

  const readFileAsDataURL = (file) => {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = () => resolve(reader.result);
      reader.onerror = () => reject(reader.error);
      reader.readAsDataURL(file);
    });
  };

  const readFileAsArrayBuffer = (file) => {
    return new Promise((resolve, reject) => {
      const reader = new FileReader();
      reader.onload = () => resolve(reader.result);
      reader.onerror = () => reject(reader.error);
      reader.readAsArrayBuffer(file);
    });
  };

  const removeFile = (index) => {
    setUploadedFiles(prev => prev.filter((_, i) => i !== index));
  };

  const generateCopy = async () => {
    setIsGenerating(true);
    setApiError(null);
    setGenerationStep('Configuring Zilla Media copy engine...');

    try {
      setGenerationStep('Assembling high-ticket psychological framework...');
      
      // Select best direct response copy structure base on category/product
      let selectedFramework = "PAS (Problem, Agitate, Solution)";
      if (category === 'Holiday' || category === 'Events') {
        selectedFramework = "AIDA (Attention, Interest, Desire, Action) + Urgency";
      } else if (product === 'Both') {
        selectedFramework = "Before-After-Bridge (BAB) structured for comparison";
      }

      // Build out reference document blocks
      const textReferences = uploadedFiles
        .filter(f => !f.isPDF)
        .map(f => `FILE: ${f.name}\nCONTENT:\n${f.content}`)
        .join('\n\n');

      const manualRef = referenceText ? `PASTED MANUAL REFERENCE:\n${referenceText}` : '';
      const urlRef = urls ? `PASTED RELEVANT URLS:\n${urls}` : '';
      const mergedReferences = [manualRef, urlRef, textReferences].filter(Boolean).join('\n\n');

      const systemInstruction = `
You are an elite, world-class direct-response copywriter specializing in high-ticket spa, hot tub, and swim spa retail. Your work is deployed for SpaSurge, a premium agency representing local showroom dealers who sell luxury wellness assets ranging from $8,000 to $45,000+. Your copy's sole objective is to move regional readers to book a showroom wet-test or physical visit.

CORE STRATEGIES:
1. BUYER PSYCHOLOGY: High-ticket wellness buyers seek deep relief (stress, muscle tension, sleep apnea, aching joints), distraction-free human connection (family time, romance), or daily physical indulgence.
2. CONVERSION STRUCTURE: Always use a ${selectedFramework} framework tailored beautifully into short, high-impact lines. Avoid reading fatigue. Maximize white space.
3. ADAPTIVE USP:
   - "Hot Tub": Focus on deep hydrotherapy, recovery sleep, intimate family spaces.
   - "Swim Spa": Focus on low-impact exercise, dual-temperature flexibility (exercise & play), replacing an expensive standard pool.
   - "Both": Seamlessly balance functional luxury, year-round exercise, and custom wet-test options.
4. DEFUSING OBJECTIONS PROACTIVELY:
   - Cost / Worth it: Emphasize financing (e.g. 0% APR), lifetime shell warranties, local factory support.
   - Maintenance Fear: Emphasize modern self-sanitizing systems (UV/Ozone), pristine automated filters, minimal chemical needs.
   - Operational/Energy Costs: Emphasize high-density full foam insulation, custom heat-trapping thermal covers.
5. NO FABRICATIONS: Strictly respect provided facts/reference document data for client promotions, guarantees, or contact information. If missing from the references, use clearly bracketed blanks like [INSERT OFFER DETAIL] or [INSERT SHOWROOM ADDRESS]. Never invent absolute offers.

Ensure the final output is absolute, valid JSON matching the schema below.
`;

      const userPrompt = `
Generate premium landing page copy blocks for our SpaSurge marketing campaign.

CLIENT METADATA:
- Client Name: ${clientName || '[Client Name]'}
- Product Range: ${product}
- Campaign Theme / Category: ${category} ${category === 'Holiday' ? `(Specific Holiday: ${holidayName})` : ''} ${category === 'Custom' ? `(Custom focus: ${customAngle})` : ''}
- Additional Strategic Guidelines: ${additionalInstructions || 'Standard direct response, high converting flow.'}

KNOWLEDGE BASE & GUIDELINES:
${mergedReferences || 'No reference documents attached. Use standard premium spa-industry high-ticket wellness copy rules with bracketed placeholders for client details.'}

OUTPUT FORMAT:
Your response must be exclusively valid JSON. Do not write any markdown blocks outside the JSON. Do not include markdown code ticks (\`\`\`json) inside the actual parsed output.

JSON Schema format to return:
{
  "hero": {
    "headline": "A punchy conversion-focused landing page headline",
    "subheadline": "Benefit-driven supporting subheadline promoting showroom wet-tests or priority pass booking",
    "cta": "Urgent CTA button text (e.g. Claim Your Showroom Wet-Test Pass)"
  },
  "problem": "Pain-agitation segment addressing back stress, restless nights, or disconnected schedules.",
  "solution": "The client's hot tub/swim spa reveal showing luxury physical outcomes and advanced design.",
  "benefits": [
    "Benefit 1 with benefit-first title: details about the body/mind outcomes",
    "Benefit 2 with benefit-first title: details about high-end product/ease",
    "Benefit 3 with benefit-first title: details about relationship/peace"
  ],
  "trust": "Factory credibility, financing highlights, local expert reassurance, design strength.",
  "objections": [
    {
      "question": "Objection Question 1 (e.g. maintenance anxiety)",
      "answer": "Simple, reassuring answer proving self-cleaning features."
    },
    {
      "question": "Objection Question 2 (e.g. power bill concerns)",
      "answer": "Compelling answer highlighting thermal containment."
    },
    {
      "question": "Objection Question 3 (e.g. selection overwhelm)",
      "answer": "Clear call to visit physical showroom for wet test."
    }
  ],
  "urgency": "Compelling call to lock in rates, showing local supply boundaries.",
  "finalCta": {
    "headline": "Enthusiastic closing headline",
    "cta": "Urgent showroom visit action CTA"
  }
}
`;

      setGenerationStep('Uploading native PDF nodes to Gemini...');
      const pdfFiles = uploadedFiles.filter(f => f.isPDF);
      
      const promptParts = [userPrompt];
      
      // Append PDFs native elements
      pdfFiles.forEach(f => {
        promptParts.push({
          inlineData: {
            mimeType: "application/pdf",
            data: f.base64
          }
        });
        promptParts.push(`This is the accompanying PDF document named "${f.name}". Use its details natively as the master source of truth for the retail business facts, prices, warranty years, and locations.`);
      });

      setGenerationStep('Calling Gemini AI optimization engines...');
      const apiKey = ""; // Canvas Runtime provides this key automatically
      const apiUrl = `https://generativelanguage.googleapis.com/v1beta/models/gemini-3-flash-preview:generateContent?key=${apiKey}`;

      const payload = {
        contents: [{
          role: "user",
          parts: promptParts.map(p => typeof p === 'string' ? { text: p } : p)
        }],
        generationConfig: {
          responseMimeType: "application/json",
          temperature: 0.25
        },
        systemInstruction: {
          parts: [{ text: systemInstruction }]
        }
      };

      const response = await fetch(apiUrl, {
        method: 'POST',
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify(payload)
      });

      if (!response.ok) {
        throw new Error(`Gemini API returned status ${response.status}`);
      }

      setGenerationStep('Structuring response nodes...');
      const result = await response.json();
      const generatedText = result.candidates?.[0]?.content?.parts?.[0]?.text;

      if (!generatedText) {
        throw new Error("No output text received from Gemini. Please verify instructions.");
      }

      // Safe JSON parsing
      const cleanedJsonText = generatedText.trim();
      const parsedData = JSON.parse(cleanedJsonText);

      // Map parsed output smoothly to states
      setGeneratedCopy({
        hero: parsedData.hero || { headline: "", subheadline: "", cta: "" },
        problem: parsedData.problem || "",
        solution: parsedData.solution || "",
        benefits: parsedData.benefits || [],
        trust: parsedData.trust || "",
        objections: parsedData.objections || [],
        urgency: parsedData.urgency || "",
        finalCta: parsedData.finalCta || { headline: "", cta: "" }
      });

      setViewState('result');
      triggerToast("High-converting copy campaign crafted!");

    } catch (err) {
      console.error(err);
      setApiError(`Generation Error: ${err.message}. Please check your connections, uploaded assets, or tweak instructions.`);
    } finally {
      setIsGenerating(false);
    }
  };

  const handleCopyFieldChange = (section, key, val) => {
    setGeneratedCopy(prev => {
      const updated = { ...prev };
      if (key === null) {
        updated[section] = val;
      } else {
        updated[section] = {
          ...updated[section],
          [key]: val
        };
      }
      return updated;
    });
  };

  const handleBenefitItemChange = (index, val) => {
    setGeneratedCopy(prev => {
      const updated = { ...prev };
      updated.benefits = [...updated.benefits];
      updated.benefits[index] = val;
      return updated;
    });
  };

  const handleObjectionChange = (index, key, val) => {
    setGeneratedCopy(prev => {
      const updated = { ...prev };
      updated.objections = updated.objections.map((obj, i) => {
        if (i === index) {
          return { ...obj, [key]: val };
        }
        return obj;
      });
      return updated;
    });
  };

  const buildPlainTextOutput = () => {
    const clientHeaderName = clientName ? clientName.toUpperCase() : "SPASURGE CLIENT";
    return `=====================================================
COPYSURGE HIGH-CONVERSION GHL LANDING PAGE COPY
CLIENT: ${clientHeaderName}
PRODUCT TARGET: ${product.toUpperCase()}
CAMPAIGN THEME: ${category.toUpperCase()}
=====================================================

--- HERO SECTION (GoHighLevel Block 1) ---
Headline: ${generatedCopy.hero.headline}
Subheadline: ${generatedCopy.hero.subheadline}
Primary Button CTA: ${generatedCopy.hero.cta}

--- THE PROBLEM SECTION (GoHighLevel Block 2) ---
${generatedCopy.problem}

--- THE SOLUTION / OFFER (GoHighLevel Block 3) ---
${generatedCopy.solution}

--- KEY BENEFITS (GoHighLevel Block 4) ---
${generatedCopy.benefits.map((b, i) => `• ${b}`).join('\n')}

--- TRUST & SHOWROOM REASSURANCE (GoHighLevel Block 5) ---
${generatedCopy.trust}

--- OBJECTIONS & FAQ ACCORDION (GoHighLevel Block 6) ---
${generatedCopy.objections.map((obj, i) => `Q: ${obj.question}\nA: ${obj.answer}`).join('\n\n')}

--- SCARCITY & URGENCY ANCHOR (GoHighLevel Block 7) ---
${generatedCopy.urgency}

--- CLOSING FINAL CTA (GoHighLevel Block 8) ---
Headline: ${generatedCopy.finalCta.headline}
Button CTA: ${generatedCopy.finalCta.cta}

=====================================================
POWERED BY ZILLA MEDIA • SPASURGE INTERNAL SYSTEM
=====================================================`;
  };

  const copyFullToClipboard = () => {
    const text = buildPlainTextOutput();
    navigator.clipboard.writeText(text).then(() => {
      setCopiedBlock('all');
      triggerToast("Complete landing page text copied!");
      setTimeout(() => setCopiedBlock(null), 3000);
    });
  };

  const copySectionToClipboard = (sectionId, content) => {
    let formattedText = "";
    if (typeof content === 'string') {
      formattedText = content;
    } else if (Array.isArray(content)) {
      formattedText = content.map(item => typeof item === 'object' ? `Q: ${item.question}\nA: ${item.answer}` : `• ${item}`).join('\n');
    } else if (typeof content === 'object') {
      formattedText = Object.entries(content).map(([k, v]) => `${k.toUpperCase()}: ${v}`).join('\n');
    }

    navigator.clipboard.writeText(formattedText).then(() => {
      setCopiedBlock(sectionId);
      triggerToast(`${sectionId.toUpperCase()} block copied!`);
      setTimeout(() => setCopiedBlock(null), 3000);
    });
  };

  const exportPDF = () => {
    if (!window.jspdf) {
      triggerToast("PDF Engine is loading. Please click in 2 seconds.");
      return;
    }

    const { jsPDF } = window.jspdf;
    const doc = new jsPDF('p', 'mm', 'a4');
    const clientTitle = clientName ? clientName : "SpaSurge Client";

    // Setup color tokens
    const primaryTeal = [14, 58, 64]; // #0e3a40
    const charcoal = [33, 33, 33];
    const lightAqua = [240, 242, 241];

    let yPosition = 20;
    const margin = 15;
    const pageWidth = doc.internal.pageSize.getWidth();
    const maxWidth = pageWidth - (margin * 2);

    // Dynamic text wrapper helper
    const addSectionText = (title, body) => {
      if (yPosition > 250) {
        doc.addPage();
        yPosition = 20;
      }

      // Title Banner
      doc.setFillColor(primaryTeal[0], primaryTeal[1], primaryTeal[2]);
      doc.rect(margin, yPosition, maxWidth, 8, 'F');
      
      doc.setTextColor(255, 255, 255);
      doc.setFont('Helvetica', 'bold');
      doc.setFontSize(10);
      doc.text(` GHL BLOCK: ${title.toUpperCase()}`, margin + 2, yPosition + 5.5);
      
      yPosition += 13;

      // Body text wrapping
      doc.setTextColor(charcoal[0], charcoal[1], charcoal[2]);
      doc.setFont('Helvetica', 'normal');
      doc.setFontSize(10);

      const splitLines = doc.splitTextToSize(body, maxWidth);
      splitLines.forEach(line => {
        if (yPosition > 275) {
          doc.addPage();
          yPosition = 20;
        }
        doc.text(line, margin, yPosition);
        yPosition += 5.5;
      });

      yPosition += 8;
    };

    // Header cover accent
    doc.setFillColor(primaryTeal[0], primaryTeal[1], primaryTeal[2]);
    doc.rect(0, 0, pageWidth, 12, 'F');
    doc.setTextColor(255, 255, 255);
    doc.setFont('Helvetica', 'bold');
    doc.setFontSize(11);
    doc.text("COPYSURGE — THE ULTIMATE COPY GENERATOR", margin, 8);

    yPosition = 25;

    // Report Header block
    doc.setTextColor(primaryTeal[0], primaryTeal[1], primaryTeal[2]);
    doc.setFontSize(18);
    doc.text("GHL Conversion Copy Architecture", margin, yPosition);
    yPosition += 6;

    doc.setFont('Helvetica', 'normal');
    doc.setFontSize(10);
    doc.setTextColor(110, 110, 110);
    doc.text(`Client Name: ${clientTitle}  |  Product Focus: ${product}  |  Theme: ${category}`, margin, yPosition);
    yPosition += 12;

    // 1. Hero Block
    const heroBody = `HEADLINE:\n${generatedCopy.hero.headline}\n\nSUBHEADLINE:\n${generatedCopy.hero.subheadline}\n\nBUTTON CTA:\n${generatedCopy.hero.cta}`;
    addSectionText("Hero Section", heroBody);

    // 2. Problem Block
    addSectionText("The Problem Hook", generatedCopy.problem);

    // 3. Solution Block
    addSectionText("The Solution / Value Offer", generatedCopy.solution);

    // 4. Benefits Block
    const benefitsBody = generatedCopy.benefits.map((b, i) => `${i + 1}. ${b}`).join('\n\n');
    addSectionText("Key Psychological Benefits", benefitsBody);

    // 5. Trust / Authority Block
    addSectionText("Credibility & Trust Foundations", generatedCopy.trust);

    // 6. Objections FAQ Block
    const objectionsBody = generatedCopy.objections.map((o, i) => `Q: ${o.question}\nA: ${o.answer}`).join('\n\n');
    addSectionText("Objection Decimation (FAQAccordion)", objectionsBody);

    // 7. Scarcity & Urgency
    addSectionText("Urgency Hook / Offer Boundaries", generatedCopy.urgency);

    // 8. Closing Hero CTA
    const closingBody = `CLOSING STATEMENT:\n${generatedCopy.finalCta.headline}\n\nACTION BUTTON:\n${generatedCopy.finalCta.cta}`;
    addSectionText("Final Call To Action Anchor", closingBody);

    // Footer overlay on all pages
    const pageCount = doc.internal.getNumberOfPages();
    for (let i = 1; i <= pageCount; i++) {
      doc.setPage(i);
      doc.setDrawColor(210, 210, 210);
      doc.line(margin, 282, pageWidth - margin, 282);
      doc.setFont('Helvetica', 'normal');
      doc.setFontSize(8);
      doc.setTextColor(130, 130, 130);
      doc.text("Powered by Zilla Media — Premium High-Ticket Client Resources", margin, 287);
      doc.text(`Page ${i} of ${pageCount}`, pageWidth - margin - 15, 287);
    }

    doc.save(`CopySurge_GHL_Copy_${clientTitle.replace(/\s+/g, '_')}.pdf`);
    triggerToast("System PDF successfully saved to downloads!");
  };

  return (
    <div className="min-h-screen bg-slate-50 flex flex-col justify-between font-sans antialiased text-slate-800">
      
      {/* Toast Notification */}
      {successToast && (
        <div className="fixed top-5 right-5 z-50 flex items-center bg-teal-900 text-white border-l-4 border-teal-400 px-4 py-3 rounded shadow-lg transition-all duration-300 transform translate-y-0">
          <CheckCircle2 className="w-5 h-5 text-teal-400 mr-2 flex-shrink-0" />
          <span className="text-sm font-medium">{successToast}</span>
        </div>
      )}

      {/* Header Panel */}
      <header className="bg-gradient-to-r from-teal-950 via-teal-900 to-slate-900 text-white border-b border-teal-800/40 py-5 px-4 md:px-8 shadow-sm">
        <div className="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
          <div className="flex items-center gap-3">
            <div className="bg-gradient-to-tr from-teal-400 to-teal-200 p-2 rounded-lg shadow-inner">
              <Sparkles className="w-6 h-6 text-teal-950" />
            </div>
            <div>
              <h1 className="text-2xl font-bold tracking-tight bg-gradient-to-r from-white to-teal-100 bg-clip-text text-transparent">
                CopySurge
              </h1>
              <p className="text-xs text-teal-300 font-medium tracking-wide uppercase">
                The Ultimate Copy Generator
              </p>
            </div>
          </div>

          <div className="flex items-center gap-2">
            <span className="bg-teal-950/80 border border-teal-700 text-teal-300 text-[10px] uppercase tracking-widest font-semibold px-2.5 py-1 rounded-full">
              Agency Edition
            </span>
            <span className="bg-emerald-950/80 border border-emerald-700 text-emerald-400 text-[10px] uppercase tracking-widest font-semibold px-2.5 py-1 rounded-full flex items-center gap-1">
              <span className="w-1.5 h-1.5 bg-emerald-400 rounded-full animate-ping"></span>
              Gemini Active
            </span>
          </div>
        </div>
      </header>

      {/* Main Content Space */}
      <main className="max-w-7xl w-full mx-auto px-4 md:px-8 py-8 flex-grow">
        
        {viewState === 'input' ? (
          /* ==================== STATE 1: INPUT FORM ==================== */
          <div className="grid grid-cols-1 lg:grid-cols-12 gap-8 items-start">
            
            {/* Left Strategic Explainer Panel */}
            <div className="lg:col-span-4 space-y-6">
              <div className="bg-gradient-to-b from-teal-950 to-slate-950 text-teal-100 rounded-2xl p-6 shadow-xl border border-teal-900/40">
                <div className="flex items-center gap-2 text-teal-300 mb-4">
                  <Layers className="w-5 h-5 text-teal-400" />
                  <h3 className="font-bold tracking-wide uppercase text-sm">SpaSurge Strategic Logic</h3>
                </div>
                
                <h4 className="text-xl font-semibold text-white mb-2">High-Ticket Psychology</h4>
                <p className="text-sm text-slate-300 leading-relaxed mb-4">
                  CopySurge writes specifically for hot tub, swim spa, and high-end sauna sales. Buying an $8k-$30k wellness appliance is a deeply considered, emotional purchase.
                </p>

                <div className="space-y-3 mt-4 text-xs">
                  <div className="flex gap-2 p-2.5 rounded bg-teal-900/30 border border-teal-800/30">
                    <Zap className="w-4 h-4 text-teal-400 flex-shrink-0" />
                    <div>
                      <strong className="text-teal-200">Emotional Leads:</strong> We never sell "jets and acrylic". We sell deep physical rejuvenation, screen-free luxury, and restorative sleep.
                    </div>
                  </div>
                  <div className="flex gap-2 p-2.5 rounded bg-teal-900/30 border border-teal-800/30">
                    <ShieldCheck className="w-4 h-4 text-teal-400 flex-shrink-0" />
                    <div>
                      <strong className="text-teal-200">Objection Decimation:</strong> Formulated to proactively defuse electrical cost fear, water upkeep anxiety, and scale options.
                    </div>
                  </div>
                </div>

                <div className="mt-6 pt-5 border-t border-teal-900/50 flex items-center justify-between">
                  <div className="text-[11px] text-slate-400">
                    System engine loaded: <span className="text-teal-300 font-mono">v4.2.16</span>
                  </div>
                  <div className="flex items-center gap-1.5 text-[11px] text-slate-300">
                    <span className="w-2 h-2 rounded-full bg-teal-400"></span> Live Showroom Specs
                  </div>
                </div>
              </div>

              {/* Informative tips widget */}
              <div className="bg-white rounded-xl p-5 border border-slate-200 shadow-sm text-xs text-slate-600 space-y-2.5">
                <div className="flex items-center gap-1.5 font-bold text-slate-800 uppercase tracking-wider text-[11px]">
                  <Info className="w-4 h-4 text-teal-600" /> Direct-Response Tip
                </div>
                <p>
                  Upload your client's dealership sheets, custom local package details, showroom street addresses, or finance offers. The Gemini engine reads them directly to prevent fabricated claims!
                </p>
              </div>
            </div>

            {/* Right Form Card Panel */}
            <div className="lg:col-span-8 bg-white rounded-2xl border border-slate-200 shadow-md p-6 md:p-8">
              <div className="border-b border-slate-100 pb-5 mb-6">
                <h2 className="text-2xl font-bold text-slate-900">Configure Landing Page Blueprint</h2>
                <p className="text-sm text-slate-500">Provide Campaign parameters, paste details, or upload documents below.</p>
              </div>

              {apiError && (
                <div className="mb-6 p-4 bg-rose-50 border border-rose-200 text-rose-800 rounded-xl flex items-start gap-3">
                  <AlertCircle className="w-5 h-5 text-rose-600 flex-shrink-0 mt-0.5" />
                  <div>
                    <h5 className="font-semibold text-sm">System Interruption</h5>
                    <p className="text-xs mt-1">{apiError}</p>
                  </div>
                </div>
              )}

              <div className="space-y-6">
                {/* Field 1: Client Name */}
                <div>
                  <label className="block text-xs font-bold uppercase tracking-wider text-slate-700 mb-2">
                    Client Name
                  </label>
                  <input
                    type="text"
                    value={clientName}
                    onChange={(e) => setClientName(e.target.value)}
                    placeholder="e.g. Spa & Hearth Retailers, AquaPro Pools"
                    className="w-full rounded-lg border border-slate-300 px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none"
                  />
                </div>

                {/* Grid for Product and Category */}
                <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
                  {/* Field 2: Product focus */}
                  <div>
                    <label className="block text-xs font-bold uppercase tracking-wider text-slate-700 mb-2">
                      Product Range Focus
                    </label>
                    <select
                      value={product}
                      onChange={(e) => setProduct(e.target.value)}
                      className="w-full rounded-lg border border-slate-300 px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none bg-white"
                    >
                      <option value="Hot Tub">Hot Tub (Therapy, sleep, romance, decompression)</option>
                      <option value="Swim Spa">Swim Spa (Exercise, low-impact, family pool option)</option>
                      <option value="Both">Both (Showroom range / versatile home spa systems)</option>
                    </select>
                  </div>

                  {/* Field 3: Category */}
                  <div>
                    <label className="block text-xs font-bold uppercase tracking-wider text-slate-700 mb-2">
                      Campaign Category Angle
                    </label>
                    <select
                      value={category}
                      onChange={(e) => {
                        setCategory(e.target.value);
                        // Reset subfields on switch
                        if (e.target.value !== 'Holiday') setHolidayName('');
                        if (e.target.value !== 'Custom') setCustomAngle('');
                      }}
                      className="w-full rounded-lg border border-slate-300 px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none bg-white"
                    >
                      <option value="Evergreen">Evergreen (Timeless showroom value, high trust)</option>
                      <option value="Holiday">Holiday (Special event seasonal hooks & genuine deadlines)</option>
                      <option value="Events">Events (Sale, Expo, Warehouse Open House, Truckload Event)</option>
                      <option value="Custom">Custom / Unique Campaign Angle</option>
                    </select>
                  </div>
                </div>

                {/* Conditional Fields based on Category */}
                {category === 'Holiday' && (
                  <div className="p-4 bg-teal-50/50 rounded-xl border border-teal-100/60 animate-fadeIn">
                    <label className="block text-xs font-bold uppercase tracking-wider text-teal-900 mb-2">
                      Which US Holiday Campaign?
                    </label>
                    <input
                      type="text"
                      value={holidayName}
                      onChange={(e) => setHolidayName(e.target.value)}
                      placeholder="e.g. Black Friday, Memorial Day, Labor Day, 4th of July"
                      className="w-full rounded-lg border border-teal-300 bg-white px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none"
                    />
                  </div>
                )}

                {category === 'Custom' && (
                  <div className="p-4 bg-teal-50/50 rounded-xl border border-teal-100/60 animate-fadeIn">
                    <label className="block text-xs font-bold uppercase tracking-wider text-teal-900 mb-2">
                      Describe Custom Angle
                    </label>
                    <input
                      type="text"
                      value={customAngle}
                      onChange={(e) => setCustomAngle(e.target.value)}
                      placeholder="e.g. Back-Pain Relief Focus, local factory trade-in clearance event"
                      className="w-full rounded-lg border border-teal-300 bg-white px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none"
                    />
                  </div>
                )}

                {/* Field 4: Reference Area, upload and URL */}
                <div className="border-t border-slate-100 pt-6">
                  <div className="flex items-center justify-between mb-2">
                    <label className="block text-xs font-bold uppercase tracking-wider text-slate-700">
                      Master References & Context Sources
                    </label>
                    <span className="text-[10px] text-slate-400">High Reliability</span>
                  </div>

                  <textarea
                    value={referenceText}
                    onChange={(e) => setReferenceText(e.target.value)}
                    rows={4}
                    placeholder="Paste client promotional package details, physical location, pricing rules, guarantees, and exact package specs..."
                    className="w-full rounded-lg border border-slate-300 px-4 py-3 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none mb-4"
                  />

                  {/* Multi-file input field */}
                  <div className="grid grid-cols-1 md:grid-cols-2 gap-4 items-start mb-4">
                    <div>
                      <div className="flex items-center justify-center w-full">
                        <label className="flex flex-col items-center justify-center w-full h-28 border-2 border-slate-300 border-dashed rounded-lg cursor-pointer bg-slate-50 hover:bg-slate-100 transition-colors">
                          <div className="flex flex-col items-center justify-center pt-4 pb-4">
                            <Upload className="w-6 h-6 text-slate-400 mb-2" />
                            <p className="text-xs text-slate-500 font-medium">Click to upload files</p>
                            <p className="text-[9px] text-slate-400">PDF (Native Reader), DOCX, TXT</p>
                          </div>
                          <input
                            type="file"
                            multiple
                            accept=".pdf,.docx,.txt"
                            onChange={handleFileUpload}
                            className="hidden"
                          />
                        </label>
                      </div>
                    </div>

                    {/* URL link parameters */}
                    <div className="space-y-2">
                      <div className="flex items-center gap-1 text-xs font-bold uppercase tracking-wider text-slate-600">
                        <Link2 className="w-4 h-4 text-slate-400" /> Direct Reference URL Link
                      </div>
                      <input
                        type="text"
                        value={urls}
                        onChange={(e) => setUrls(e.target.value)}
                        placeholder="Paste dealership pages, competitor URLs, e.g. https://www.clientdealer.com"
                        className="w-full rounded-lg border border-slate-300 px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none bg-slate-50"
                      />
                      <p className="text-[10px] text-slate-400 italic">
                        Uploaded docs and pasted text are the most reliable source. Links are used as supporting context only.
                      </p>
                    </div>
                  </div>

                  {/* Uploaded File List Display */}
                  {uploadedFiles.length > 0 && (
                    <div className="bg-slate-100/80 rounded-xl p-3 border border-slate-200/60 space-y-2 mb-4">
                      <div className="text-[10px] uppercase font-bold text-slate-500 tracking-wider px-1">
                        Parsed Campaign Sources ({uploadedFiles.length})
                      </div>
                      <div className="space-y-1">
                        {uploadedFiles.map((f, i) => (
                          <div key={i} className="flex items-center justify-between bg-white px-3 py-1.5 rounded-lg border border-slate-200 text-xs">
                            <div className="flex items-center gap-2 text-slate-700 font-medium truncate max-w-[85%]">
                              {f.isPDF ? (
                                <FileCode className="w-4 h-4 text-red-500" />
                              ) : (
                                <FileText className="w-4 h-4 text-teal-600" />
                              )}
                              <span className="truncate">{f.name}</span>
                              <span className="text-[9px] text-slate-400">({f.size})</span>
                            </div>
                            <button
                              type="button"
                              onClick={() => removeFile(i)}
                              className="text-slate-400 hover:text-rose-600 p-1 transition-colors"
                            >
                              <Trash2 className="w-3.5 h-3.5" />
                            </button>
                          </div>
                        ))}
                      </div>
                    </div>
                  )}
                </div>

                {/* Field 5: Additional Instructions */}
                <div className="border-t border-slate-100 pt-6">
                  <label className="block text-xs font-bold uppercase tracking-wider text-slate-700 mb-2">
                    Additional Instructions / Creative Directives
                  </label>
                  <textarea
                    value={additionalInstructions}
                    onChange={(e) => setAdditionalInstructions(e.target.value)}
                    rows={2}
                    placeholder="Optional: Specify CTA wording, exact colors/themes, target towns/neighborhoods, or structural goals..."
                    className="w-full rounded-lg border border-slate-300 px-4 py-2.5 text-sm focus:border-teal-600 focus:ring-1 focus:ring-teal-600 focus:outline-none"
                  />
                </div>

                {/* Submission Action Grid */}
                <div className="pt-4">
                  <button
                    onClick={generateCopy}
                    disabled={isGenerating}
                    className="w-full bg-gradient-to-r from-teal-950 to-teal-800 text-white rounded-xl py-4 font-bold tracking-wide uppercase text-sm hover:from-teal-900 hover:to-teal-700 focus:ring-2 focus:ring-teal-500 focus:outline-none active:scale-[0.99] shadow-md transition-all flex items-center justify-center gap-2 disabled:opacity-50"
                  >
                    {isGenerating ? (
                      <>
                        <RefreshCw className="w-5 h-5 animate-spin text-teal-300" />
                        <span>{generationStep}</span>
                      </>
                    ) : (
                      <>
                        <Sparkles className="w-5 h-5 text-teal-300" />
                        <span>Generate High-Converting GHL Funnel Copy</span>
                      </>
                    )}
                  </button>
                </div>

              </div>
            </div>

          </div>
        ) : (
          /* ==================== STATE 2: RESULT & PREVIEW ==================== */
          <div className="space-y-8 animate-fadeIn">
            
            {/* Control Panel Block */}
            <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-4 md:p-6 flex flex-col md:flex-row justify-between items-center gap-4">
              <div>
                <h2 className="text-xl font-bold text-slate-900 flex items-center gap-2">
                  <Eye className="w-5 h-5 text-teal-600" /> Live Funnel Copy Architect
                </h2>
                <p className="text-xs text-slate-500 mt-1">
                  Editable inline. Direct simulation of matching sections for Google Docs or GoHighLevel insertion.
                </p>
              </div>

              <div className="flex flex-wrap gap-2 w-full md:w-auto">
                <button
                  onClick={copyFullToClipboard}
                  className="flex-1 md:flex-initial bg-teal-900 hover:bg-teal-800 text-white text-xs font-bold uppercase tracking-wider px-4 py-2.5 rounded-lg transition-all flex items-center justify-center gap-2 shadow"
                >
                  {copiedBlock === 'all' ? <Check className="w-4 h-4 text-emerald-400" /> : <Copy className="w-4 h-4" />}
                  <span>{copiedBlock === 'all' ? 'Copied Full Campaign' : 'Copy Full Copy for Google Docs'}</span>
                </button>

                <button
                  onClick={exportPDF}
                  className="flex-1 md:flex-initial bg-slate-900 hover:bg-slate-800 text-white text-xs font-bold uppercase tracking-wider px-4 py-2.5 rounded-lg transition-all flex items-center justify-center gap-2 shadow"
                >
                  <FileDown className="w-4 h-4" />
                  <span>Download Blueprint PDF</span>
                </button>

                <button
                  onClick={() => setViewState('input')}
                  className="flex-1 md:flex-initial bg-white border border-slate-300 hover:bg-slate-50 text-slate-700 text-xs font-bold uppercase tracking-wider px-4 py-2.5 rounded-lg transition-all flex items-center justify-center gap-2 shadow"
                >
                  <RefreshCw className="w-4 h-4" />
                  <span>Tweak Parameters</span>
                </button>
              </div>
            </div>

            {/* Simulated Live Funnel Blocks */}
            <div className="space-y-12">

              {/* BLOCK 1: Hero Block */}
              <div className="bg-gradient-to-b from-teal-950 via-teal-900 to-slate-900 text-white rounded-3xl p-8 md:p-12 shadow-xl relative border border-teal-800 overflow-hidden">
                <div className="absolute right-4 top-4 bg-teal-500/20 text-teal-300 border border-teal-500/20 text-[10px] tracking-widest font-bold uppercase py-1 px-3 rounded-full">
                  GHL BLOCK 1: HERO CONTAINER
                </div>

                <div className="max-w-3xl mx-auto text-center space-y-6 pt-4">
                  <div className="inline-block bg-teal-400/10 text-teal-300 border border-teal-400/20 text-xs font-semibold px-4 py-1.5 rounded-full uppercase tracking-wider">
                    Showroom Booking Event
                  </div>
                  
                  {/* Headline Editable */}
                  <textarea
                    value={generatedCopy.hero.headline}
                    onChange={(e) => handleCopyFieldChange('hero', 'headline', e.target.value)}
                    rows={2}
                    className="w-full bg-transparent text-white text-3xl md:text-4xl font-extrabold text-center tracking-tight focus:bg-teal-900/40 p-2 rounded-lg resize-none border border-transparent focus:border-teal-400 focus:outline-none"
                    placeholder="Main Campaign Headline"
                  />

                  {/* Subheadline Editable */}
                  <textarea
                    value={generatedCopy.hero.subheadline}
                    onChange={(e) => handleCopyFieldChange('hero', 'subheadline', e.target.value)}
                    rows={3}
                    className="w-full bg-transparent text-teal-100 text-sm md:text-base leading-relaxed text-center max-w-2xl mx-auto focus:bg-teal-900/40 p-2 rounded-lg resize-none border border-transparent focus:border-teal-400 focus:outline-none"
                    placeholder="Supporting subheadline"
                  />

                  {/* CTA Editable */}
                  <div className="pt-4 flex flex-col items-center gap-3">
                    <input
                      type="text"
                      value={generatedCopy.hero.cta}
                      onChange={(e) => handleCopyFieldChange('hero', 'cta', e.target.value)}
                      className="bg-gradient-to-r from-teal-400 to-teal-300 text-teal-950 hover:from-teal-300 hover:to-teal-200 font-extrabold text-sm uppercase tracking-wider py-3.5 px-8 rounded-xl shadow-lg focus:outline-none border-2 border-teal-200 text-center max-w-md"
                      placeholder="Button CTA Wording"
                    />
                    <p className="text-[10px] text-teal-400 italic">★ Fast showroom reservation voucher secured</p>
                  </div>
                </div>

                {/* Section Action Trigger */}
                <div className="mt-8 pt-6 border-t border-teal-800/60 flex justify-between items-center text-xs text-teal-300">
                  <span>Sections mapped to GoHighLevel templates perfectly</span>
                  <button
                    onClick={() => copySectionToClipboard('hero', generatedCopy.hero)}
                    className="hover:text-white flex items-center gap-1.5 transition-colors font-semibold"
                  >
                    {copiedBlock === 'hero' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                    <span>{copiedBlock === 'hero' ? 'Section Copied' : 'Copy Hero Block'}</span>
                  </button>
                </div>
              </div>

              {/* Two Column Grid for Problem & Solution */}
              <div className="grid grid-cols-1 lg:grid-cols-2 gap-8">
                
                {/* BLOCK 2: The Problem */}
                <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 md:p-8 flex flex-col justify-between">
                  <div>
                    <div className="flex items-center justify-between mb-4">
                      <div className="flex items-center gap-2 text-rose-700">
                        <Flame className="w-5 h-5" />
                        <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 2: THE PROBLEM</span>
                      </div>
                      <span className="text-[10px] text-slate-400 italic font-medium">PAS Phase 1 (Agitate)</span>
                    </div>

                    <h3 className="text-lg font-bold text-slate-900 mb-3">Target Pain/Agitation Angle</h3>
                    <textarea
                      value={generatedCopy.problem}
                      onChange={(e) => handleCopyFieldChange('problem', null, e.target.value)}
                      rows={6}
                      className="w-full bg-slate-50 text-slate-700 text-sm leading-relaxed p-3.5 rounded-xl border border-slate-200 focus:bg-white focus:border-teal-600 focus:outline-none resize-none"
                    />
                  </div>

                  <div className="mt-6 pt-4 border-t border-slate-100 flex justify-end text-xs text-slate-400">
                    <button
                      onClick={() => copySectionToClipboard('problem', generatedCopy.problem)}
                      className="hover:text-slate-800 flex items-center gap-1.5 transition-colors font-semibold"
                    >
                      {copiedBlock === 'problem' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                      <span>Copy Block 2</span>
                    </button>
                  </div>
                </div>

                {/* BLOCK 3: The Solution / Offer */}
                <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 md:p-8 flex flex-col justify-between">
                  <div>
                    <div className="flex items-center justify-between mb-4">
                      <div className="flex items-center gap-2 text-teal-800">
                        <Zap className="w-5 h-5 text-teal-600" />
                        <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 3: THE SOLUTION / OFFER</span>
                      </div>
                      <span className="text-[10px] text-slate-400 italic font-medium">PAS Phase 2 (Reveal)</span>
                    </div>

                    <h3 className="text-lg font-bold text-slate-900 mb-3">Premium Product Reveal & Hook</h3>
                    <textarea
                      value={generatedCopy.solution}
                      onChange={(e) => handleCopyFieldChange('solution', null, e.target.value)}
                      rows={6}
                      className="w-full bg-slate-50 text-slate-700 text-sm leading-relaxed p-3.5 rounded-xl border border-slate-200 focus:bg-white focus:border-teal-600 focus:outline-none resize-none"
                    />
                  </div>

                  <div className="mt-6 pt-4 border-t border-slate-100 flex justify-end text-xs text-slate-400">
                    <button
                      onClick={() => copySectionToClipboard('solution', generatedCopy.solution)}
                      className="hover:text-slate-800 flex items-center gap-1.5 transition-colors font-semibold"
                    >
                      {copiedBlock === 'solution' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                      <span>Copy Block 3</span>
                    </button>
                  </div>
                </div>

              </div>

              {/* BLOCK 4: Key Benefits Section */}
              <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 md:p-8">
                <div className="flex items-center justify-between mb-6 border-b border-slate-100 pb-4">
                  <div className="flex items-center gap-2 text-slate-800">
                    <Layers className="w-5 h-5 text-teal-600" />
                    <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 4: BENEFIT GRID</span>
                  </div>
                  <button
                    onClick={() => copySectionToClipboard('benefits', generatedCopy.benefits)}
                    className="text-slate-400 hover:text-slate-800 text-xs flex items-center gap-1 transition-colors font-semibold"
                  >
                    {copiedBlock === 'benefits' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                    <span>Copy Benefits List</span>
                  </button>
                </div>

                <div className="space-y-4">
                  {generatedCopy.benefits.map((b, idx) => (
                    <div key={idx} className="flex gap-3 items-start bg-slate-50 p-4 rounded-xl border border-slate-200/60 hover:border-slate-300 transition-colors">
                      <div className="bg-teal-100 text-teal-800 w-6 h-6 rounded-full flex items-center justify-center text-xs font-bold flex-shrink-0 mt-0.5">
                        {idx + 1}
                      </div>
                      <div className="w-full">
                        <textarea
                          value={b}
                          onChange={(e) => handleBenefitItemChange(idx, e.target.value)}
                          rows={2}
                          className="w-full bg-transparent text-slate-700 text-sm leading-relaxed focus:bg-white p-1 rounded focus:outline-none focus:ring-1 focus:ring-teal-600"
                        />
                      </div>
                    </div>
                  ))}
                </div>
              </div>

              {/* BLOCK 5: Trust and Showroom Credibility */}
              <div className="bg-slate-900 text-slate-100 rounded-2xl p-6 md:p-8 border border-slate-800">
                <div className="flex items-center justify-between mb-4">
                  <div className="flex items-center gap-2 text-teal-400">
                    <ShieldCheck className="w-5 h-5" />
                    <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 5: TRUST, SOCIAL PROOF & WARRANTIES</span>
                  </div>
                  <button
                    onClick={() => copySectionToClipboard('trust', generatedCopy.trust)}
                    className="text-slate-400 hover:text-white text-xs flex items-center gap-1 transition-colors font-semibold"
                  >
                    {copiedBlock === 'trust' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                    <span>Copy Block 5</span>
                  </button>
                </div>

                <h3 className="text-lg font-bold text-white mb-3">Reassurance Statement (Showroom & Guarantee Trust)</h3>
                <textarea
                  value={generatedCopy.trust}
                  onChange={(e) => handleCopyFieldChange('trust', null, e.target.value)}
                  rows={4}
                  className="w-full bg-slate-850 text-slate-300 text-sm leading-relaxed p-4 rounded-xl border border-slate-800 focus:bg-slate-950 focus:border-teal-400 focus:outline-none resize-none"
                />
              </div>

              {/* BLOCK 6: FAQ Objection Handling Accordion */}
              <div className="bg-white rounded-2xl border border-slate-200 shadow-sm p-6 md:p-8">
                <div className="flex items-center justify-between mb-6 border-b border-slate-100 pb-4">
                  <div className="flex items-center gap-2 text-slate-800">
                    <HelpCircle className="w-5 h-5 text-teal-600" />
                    <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 6: OBJECTION-DECIMATION FAQ</span>
                  </div>
                  <button
                    onClick={() => copySectionToClipboard('objections', generatedCopy.objections)}
                    className="text-slate-400 hover:text-slate-800 text-xs flex items-center gap-1 transition-colors font-semibold"
                  >
                    {copiedBlock === 'objections' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                    <span>Copy FAQ Data</span>
                  </button>
                </div>

                <div className="space-y-6">
                  {generatedCopy.objections.map((o, idx) => (
                    <div key={idx} className="bg-slate-50 rounded-xl p-4 border border-slate-200/80 space-y-3">
                      <div>
                        <span className="text-[10px] uppercase font-bold text-slate-400 tracking-wider">Objection Question {idx + 1}</span>
                        <input
                          type="text"
                          value={o.question}
                          onChange={(e) => handleObjectionChange(idx, 'question', e.target.value)}
                          className="w-full bg-transparent font-bold text-slate-800 text-sm p-1 border-b border-transparent focus:border-teal-600 focus:outline-none"
                        />
                      </div>
                      <div>
                        <span className="text-[10px] uppercase font-bold text-teal-600 tracking-wider">Dynamic Reassurance Answer</span>
                        <textarea
                          value={o.answer}
                          onChange={(e) => handleObjectionChange(idx, 'answer', e.target.value)}
                          rows={2}
                          className="w-full bg-transparent text-slate-600 text-xs p-1 focus:bg-white rounded focus:outline-none focus:ring-1 focus:ring-teal-600"
                        />
                      </div>
                    </div>
                  ))}
                </div>
              </div>

              {/* Grid block for Scarcity Urgency and Final CTA */}
              <div className="grid grid-cols-1 lg:grid-cols-12 gap-8">
                
                {/* BLOCK 7: Scarcity & Urgency Detail */}
                <div className="lg:col-span-5 bg-white rounded-2xl border border-slate-200 shadow-sm p-6 flex flex-col justify-between">
                  <div>
                    <div className="flex items-center justify-between mb-4">
                      <div className="flex items-center gap-2 text-amber-700">
                        <Flame className="w-5 h-5" />
                        <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 7: URGENCY & SCARCITY</span>
                      </div>
                      <span className="text-[9px] text-slate-400 italic">Seasonal Hook</span>
                    </div>

                    <h3 className="text-sm font-bold text-slate-900 mb-2">Campaign Offer Urgency</h3>
                    <textarea
                      value={generatedCopy.urgency}
                      onChange={(e) => handleCopyFieldChange('urgency', null, e.target.value)}
                      rows={5}
                      className="w-full bg-slate-50 text-slate-700 text-xs leading-relaxed p-3 rounded-lg border border-slate-200 focus:bg-white focus:border-teal-600 focus:outline-none resize-none"
                    />
                  </div>

                  <div className="mt-4 pt-3 border-t border-slate-100 flex justify-end">
                    <button
                      onClick={() => copySectionToClipboard('urgency', generatedCopy.urgency)}
                      className="text-slate-400 hover:text-slate-700 text-xs flex items-center gap-1 transition-colors font-semibold"
                    >
                      {copiedBlock === 'urgency' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                      <span>Copy Block 7</span>
                    </button>
                  </div>
                </div>

                {/* BLOCK 8: Final CTA */}
                <div className="lg:col-span-7 bg-gradient-to-tr from-slate-900 to-teal-950 text-white rounded-2xl p-6 flex flex-col justify-between border border-slate-800">
                  <div>
                    <div className="flex items-center justify-between mb-4">
                      <div className="flex items-center gap-2 text-teal-400">
                        <Zap className="w-5 h-5" />
                        <span className="text-xs uppercase font-extrabold tracking-widest">GHL BLOCK 8: FINAL CTA ANCHOR</span>
                      </div>
                      <span className="text-[9px] text-teal-400 tracking-widest font-bold">CONVERSION</span>
                    </div>

                    <div className="space-y-4">
                      <div>
                        <span className="text-[9px] text-slate-400 uppercase tracking-wider block mb-1">Closing CTA Pitch Headline</span>
                        <input
                          type="text"
                          value={generatedCopy.finalCta.headline}
                          onChange={(e) => handleCopyFieldChange('finalCta', 'headline', e.target.value)}
                          className="w-full bg-transparent font-bold text-white text-base p-1 border-b border-transparent focus:border-teal-400 focus:outline-none"
                        />
                      </div>

                      <div>
                        <span className="text-[9px] text-slate-400 uppercase tracking-wider block mb-1">Final Button Text</span>
                        <input
                          type="text"
                          value={generatedCopy.finalCta.cta}
                          onChange={(e) => handleCopyFieldChange('finalCta', 'cta', e.target.value)}
                          className="w-full max-w-sm bg-teal-400 hover:bg-teal-300 text-teal-950 font-extrabold text-xs uppercase tracking-wider py-2 px-4 rounded shadow-md focus:outline-none border-b-2 border-teal-500 text-center"
                        />
                      </div>
                    </div>
                  </div>

                  <div className="mt-4 pt-3 border-t border-teal-900 flex justify-end">
                    <button
                      onClick={() => copySectionToClipboard('finalCta', generatedCopy.finalCta)}
                      className="text-slate-400 hover:text-white text-xs flex items-center gap-1 transition-colors font-semibold"
                    >
                      {copiedBlock === 'finalCta' ? <Check className="w-3.5 h-3.5" /> : <Copy className="w-3.5 h-3.5" />}
                      <span>Copy Block 8</span>
                    </button>
                  </div>
                </div>

              </div>

            </div>

          </div>
        )}

      </main>

      {/* Persistent Agency Footer */}
      <footer className="bg-slate-900 border-t border-slate-800 text-slate-500 py-6 px-4 md:px-8 text-center text-xs">
        <div className="max-w-7xl mx-auto flex flex-col sm:flex-row items-center justify-between gap-4">
          <p className="font-medium tracking-wide uppercase text-[10px]">
            Powered by Zilla Media
          </p>
          <p className="text-slate-600">
            Internal Marketing Suite Asset • strictly confidential client records only
          </p>
        </div>
      </footer>

    </div>
  );
}
